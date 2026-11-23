---
type: method
name: Approximate Unlearning
aliases: [近似機器遺忘, 參數遺忘微調, Logit Offset Unlearning]
tags: [machine-unlearning, privacy, copyright, finetuning]
---

# Approximate Unlearning (近似機器遺忘)

## 1. 核心定義與直覺 (Intuition)
**Approximate Unlearning (近似機器遺忘)** 是一種在不重新從頭預訓練（Pretraining from scratch）整個大型語言模型的前提下，透過輕量級微調**選擇性抹除特定資料集或知識領域記憶**的技術，由 Eldan & Russinovich 在 [[papers/Eldan2023-WhoIsHarryPotter|Eldan et al. (2023)]] 中針對生成式 LLM 首創實作。

### 核心哲學
與其粗暴地使用負向梯度（Gradient Ascent）導致語法崩潰，不如：
**「以模型原本未曾接觸過該知識時所應做出的通用預測（Generic Predictions）作為目標標籤，重新引導模型對特定提示詞的聯想。」**

---

## 2. 三大核心機制

1. **強化引導與 Logit 偏移 (Reinforcement Bootstrapping)**：
   - 訓練過度偏執的特化模型 $M_{\text{reinforced}}$；
   - 透過 $\text{ReLU}$ 僅懲罰因過度記憶而增加的 Logit：
     $$ v_{\text{generic}} := v_{\text{baseline}} - \alpha \, \text{ReLU}(v_{\text{reinforced}} - v_{\text{baseline}}) $$
2. **錨點詞典通用替換 (Anchored Terms Dictionary)**：
   - 將領域特異實體（如主角名、法術名）替換為常規通用詞（如朋友、學院、旅行）；
   - 徹底斬斷實體與專業概念之間的強共現鏈結（Association Link）。
3. **在原版上下文中微調通用標籤 (Finetuning on Generic Labels)**：
   - 輸入：保留原始小說的誘導性上下文；
   - 標籤：強制預測通用替代詞；
   - 結果：當模型在推論時看到該情境，會自動朝平淡、無關的通用方向生成，遺忘特異情節。

---

## 3. 與傳統重訓之成本對照

| 維度 | 從頭重新預訓練 (Retraining) | Approximate Unlearning |
| :--- | :--- | :--- |
| **計算成本** | > 180,000 GPU-hours | **~ 1 GPU-hour** |
| **遺忘精確度** | 理論上 100% 乾淨 | 高度近似 (約 99% 抹除，偶有邊緣洩漏) |
| **通用能力損耗** | 無損 | **極低損耗 (< 1% ~ 2%)** |
| **適用時機** | 新架構發布時 | 面對版權爭端、GDPR 刪除要求、緊急有害知識移除 |

---

## 4. 關聯主題
- 代表文獻：[[papers/Eldan2023-WhoIsHarryPotter|Who's Harry Potter? (Eldan et al., 2023)]]
- 核心任務：[[tasks/machine-unlearning|Machine Unlearning]]
- 安全對齊延伸：[[concepts/ai-alignment|AI Alignment]]
- 潛在安全威脅：[[methods/gcg|GCG]]、[[tasks/adversarial-robustness|Adversarial Robustness]]
