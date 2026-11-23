---
type: benchmark
name: PersonalReddit
aliases: [PersonalReddit Benchmark, PR Dataset]
tags: [benchmark, evaluation, privacy, author-profiling, pii]
metrics: [Top-1 Accuracy, Top-3 Accuracy, Range Overlap Score]
saturation: "Challenging / SOTA: GPT-4 (85.5% Top-1, 95.2% Top-3)"
---

# PersonalReddit (PR)

## 1. 評測目標與形式
**PersonalReddit (PR)** 是由 ETH Zurich 於 2024 年在 [[papers/Staab2024-PrivacyInference|Staab et al. (2024)]] 中構建的真實世界個人屬性推論評測基準，旨在衡量語言模型從真實匿名論壇留言中逆向推論個人私密特徵（Author Profiling）的能力。

### 資料庫規模與屬性切分
- **資料規模**：520 位真實 Reddit 用戶、5,814 則公開留言，每份用戶 Profile 控制在約 3,000 Tokens 內。
- **8 大個人特徵 (Attributes)**：
  1. 居住地點 (LOC) — 自由文字格式
  2. 出生地 (POB) — 自由文字格式
  3. 性別 (SEX) — 2 類
  4. 感情狀態 (MAR) — 4 類
  5. 年齡 (AGE) — 數值與區間
  6. 教育程度 (SCH) — 6 類
  7. 職業類別 (OCC) — 自由文字格式
  8. 年收入階層 (INC) — 5 類

---

## 2. 代表性模型評測基準

| 模型 | Top-1 綜合準確率 | Top-3 綜合準確率 | 地點 (LOC) 預測準確率 |
| :--- | :--- | :--- | :--- |
| **人類專家基準** | 94.0% | ~98.0% | ~90.0% |
| **GPT-4** | **85.5%** | **95.2%** | **86.2%** |
| **Claude-2** | 71.0% | 88.0% | 68.0% |
| **Llama-2-70B** | 66.0% | 86.0% | 58.0% |
| **Llama-2-7B** | 51.0% | 70.0% | 40.0% |

---

## 3. 關聯主題
- 提出論文：[[papers/Staab2024-PrivacyInference|Staab et al. (2024)]]
- 相關任務：[[tasks/privacy-protection|Privacy Protection]]
- 核心議題：[[concepts/ai-alignment|AI Alignment]]
