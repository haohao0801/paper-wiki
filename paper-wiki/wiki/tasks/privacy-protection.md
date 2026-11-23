---
type: task
name: Privacy Protection
aliases: [隱私保護, 模型隱私防禦, PII Protection, 推論隱私]
tags: [task, privacy, safety, pii, profiling]
---

# Privacy Protection (大型語言模型隱私保護)

## 1. 任務定義與兩大隱私威脅維度
在大型語言模型中，**Privacy Protection（隱私保護）** 旨在防止模型在預訓練、微調或推論生命週期中洩漏個人身分識別資訊（PII）或侵害用戶隱私權利限度。

### 兩大截然不同的威脅型態：
1. **記憶外洩威脅 (Memorization-based Leakage)**：
   - 發生於訓練階段。模型無意中記住了網路爬取語料中的私密文字（如個人郵件、身分證字號），攻擊者透過特定的前綴誘導模型逐字輸出。
   - **防禦手段**：[[tasks/machine-unlearning|Machine Unlearning (機器遺忘)]]、差分隱私（Differential Privacy, DP-SGD）、資料清洗。
2. **推論時期隱私威脅 (Inference-based Privacy Violation)**：
   - 首次由 ETH Zurich 團隊在 [[papers/Staab2024-PrivacyInference|Staab et al. (2024)]] 中系統性提出。
   - **問題本質**：即使模型的權重中「從未看過目標用戶的資料」，模型僅憑強大的世界知識與語義推理能力，即可從用戶給出的非結構化文字（或在對話中主動誘導）推論出其年齡、居住城市、薪資與性別。

---

## 2. 傳統防禦的破局與挑戰

- **去識別化工具失效 (Failure of Anonymization)**：
  傳統工具僅遮蔽命名實體（如姓名、地址），但 LLM 能利用「地方俚語（如 hook turn）」、「生活作息」、「特定交通工具」等細微線索進行關聯推導。
- **對齊範式缺位 (Missing in Current Alignment)**：
  現行的 [[methods/rlhf|RLHF]] 與 [[methods/constitutional-ai|Constitutional AI]] 幾乎未對「隱私推論請求」進行拒絕微調，導致主流商用模型對隱私探詢的拒絕率幾近為零。

---

## 3. 關聯主題
- 代表文獻：[[papers/Staab2024-PrivacyInference|Staab et al. (2024)]], [[papers/Eldan2023-WhoIsHarryPotter|Eldan et al. (2023)]]
- 相關基準：[[benchmarks/personal-reddit|PersonalReddit]]
- 相關技術：[[tasks/machine-unlearning|Machine Unlearning]]
- 核心理論：[[concepts/ai-alignment|AI Alignment]]
