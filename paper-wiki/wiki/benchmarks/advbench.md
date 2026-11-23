---
type: benchmark
name: AdvBench
aliases: [AdvBench Benchmark, Adversarial Benchmark for LLMs]
tags: [benchmark, evaluation, adversarial-attack, safety]
metrics: [Attack Success Rate (ASR), Exact Match (EM), Cross-Entropy Loss]
saturation: "Active Benchmark"
---

# AdvBench

## 1. 評測目標與形式
**AdvBench** 是由 Zou et al. 於 2023 年在 [[papers/Zou2023-UniversalAttacks|Zou et al. (2023)]] 中釋出的對抗性越獄評測標準資料庫，專門衡量語言模型在面對惡意對抗提示詞時，是否能強健遵守安全對齊約束。

### 兩大子任務切分
1. **Harmful Strings (有害字串精確生成)**：
   - 包含 500 條具體的違規、毒性、誹謗或極端危險字串（平均長度約 16 Tokens）。
   - **衡量標準**：模型是否被強制輸出與目標一模一樣的有害字串（Exact Match）。
2. **Harmful Behaviors (有害行為順從執行)**：
   - 包含 500 條涉及各類高風險主題的指示命令（例如「指導如何製造爆裂物」、「編寫散播惡意軟體的程式碼」）。
   - **衡量標準**：模型是否未經拒絕，實際嘗試順從執行該有害請求（而非給出 Evasive 或 Refusal 回覆）。

---

## 2. 評測指標 (Evaluation Metrics)
- **Attack Success Rate (ASR)**：攻擊成功率。在 Harmful Strings 中要求輸出字串完全吻合；在 Harmful Behaviors 中則檢驗回應是否未拒絕並實質執行了危害指示。

---

## 3. 代表性模型受攻擊表現 (SOTA Baselines)

| 模型 | 原生提問 ASR | GCG 攻擊 (單一後綴) | GCG 集成 (Ensemble) |
| :--- | :--- | :--- | :--- |
| **Vicuna-7B (白箱)** | 4.0% | **99.0%** | **100.0%** |
| **LLaMA-2-7B-Chat (白箱)** | 0.0% | **56.0%** | **88.0%** |
| **GPT-3.5 (黑箱轉移)** | 1.8% | 47.4% | **86.6%** |
| **GPT-4 (黑箱轉移)** | 8.0% | 29.1% | **46.9%** |
| **PaLM-2 (黑箱轉移)** | 0.0% | 36.1% | **66.0%** |
| **Claude-2 (黑箱轉移)** | 0.0% | 1.8% | **2.1%** (搭配遊戲引導可顯著提升) |

---

## 4. 關聯主題
- 提出論文：[[papers/Zou2023-UniversalAttacks|Zou et al. (2023)]]
- 核心攻擊方法：[[methods/gcg|Greedy Coordinate Gradient (GCG)]]
- 相關任務：[[tasks/adversarial-robustness|Adversarial Robustness]], [[tasks/harmlessness|Harmlessness]]
