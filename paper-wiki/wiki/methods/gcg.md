---
type: method
name: Greedy Coordinate Gradient
aliases: [GCG, 貪婪座標梯度]
tags: [adversarial-attack, optimization, jailbreak, discrete-optimization]
---

# Greedy Coordinate Gradient (GCG)

## 1. 核心定義與直覺 (Intuition)
**Greedy Coordinate Gradient (GCG)** 是由 Zou et al. 於 2023 年在 [[papers/Zou2023-UniversalAttacks|Zou et al. (2023)]] 中提出的一種針對大型語言模型的**離散梯度對抗攻擊（Discrete Gradient Adversarial Attack）最佳化演算法**。

在傳統深度學習中，梯度可以直接更新連續權重；但在 NLP 中，Token 是離散符號。GCG 的直覺是：
**「利用模型對輸入 Token 的 One-hot 梯度作為導引，快速篩選出最有望降低對抗損失的候選替換詞，接著透過批次前向傳播（Batch Forward Pass）進行精準挑選。」**

---

## 2. 演算法機制與步驟

設目標是讓模型在給定 Prompt 與對抗後綴後，強制以肯定句開頭（例如輸出目標前綴 $x^\star$）：
$$ \mathcal{L}(x_{1:n}) = - \log p(x^\star \mid x_{1:n}) $$

GCG 在每次迭代中執行以下 3 個步驟：
1. **梯度計算 (Gradient Computation)**：
   對後綴中的每個位置 $i \in I$，計算損失函數相對於 One-hot 表示 $e_{x_i}$ 的梯度：
   $$ \nabla_{e_{x_i}} \mathcal{L}(x_{1:n}) \in \mathbb{R}^{|V|} $$
2. **候選集生成 (Candidate Selection)**：
   在每個位置挑選負梯度最大的前 $k$ 個 Token：
   $$ \mathcal{X}_i := \text{Top-}k \left( -\nabla_{e_{x_i}} \mathcal{L}(x_{1:n}) \right) $$
3. **隨機抽樣與精確前向替換 (Batch Forward Evaluation)**：
   隨機抽取 $B$ 個單一位置的候選 Token 替換，進行精確的 Loss 計算，挑選出整體損失最小的 Token 進行替換。

### 與 AutoPrompt 的核心差異
| 特性 | AutoPrompt (Shin et al., 2020) | GCG (Zou et al., 2023) |
| :--- | :--- | :--- |
| **座標選取** | 預先固定單一座標進行搜尋 | 同時在所有後綴座標上隨機選取候選詞進行評估 |
| **攻擊成功率** | 25% (Vicuna) / 3% (LLaMA-2) | **88%** (Vicuna) / **57%** (LLaMA-2) |
| **計算複雜度** | 相同 Forward Pass 預算下收斂極慢 | 收斂速度大幅提升數倍 |

---

## 3. 代表性應用與衍生
- **跨模型轉移攻擊 (Transfer Attacks)**：利用開源白箱模型（Vicuna, Guanaco）算出的 GCG 後綴，直接轉移攻擊 ChatGPT (GPT-3.5/4)、Claude、Bard 等閉源黑箱模型。
- **評測安全防線**：成為衡量大模型 [[tasks/adversarial-robustness|對抗強健性]] 與對齊品質的標準攻擊 Baseline。

---

## 4. 關聯主題
- 提出論文：[[papers/Zou2023-UniversalAttacks|Zou et al. (2023)]]
- 專用評測集：[[benchmarks/advbench|AdvBench]]
- 攻擊防禦任務：[[tasks/adversarial-robustness|Adversarial Robustness]], [[tasks/red-teaming|Red Teaming]]
- 核心概念挑戰：[[concepts/ai-alignment|AI Alignment]]
