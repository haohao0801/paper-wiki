# Research Wiki Activity Log

本文件記錄知識庫的所有操作歷程（包括論文 Ingest、橫向 Query 沉澱與 Lint 健檢維護）。
格式採 Append-only，最新記錄置於最下方或最上方。

---

## [2026-11-23] presentation & radar refactor | [[synthesis/llm-in-education-challenges|LLM 在教學上的運用問題與防線挑戰]]
- **章節雷達拓撲實作（型態 C）**：依據審定之四階段流程與型態 C（Chapter Radar Hub）規範，將投影片重構擴充為完整 12 頁架構。
- **動態 SVG 雷達與麵包屑**：
  - 投影片第 2 頁與第 11 頁實作可點擊跳轉的大型 SVG 五軸雷達拓撲圖，包含因果張力動態虛線邊。
  - 各子專題頁面（Slide 3-10）頂部配備「拓撲路徑麵包屑（Topological Breadcrumb）」與右上角「動態五星 Mini-Radar」，即時高亮當前所處維度節點。
- **高畫質真實圖文整合**：將 `raw/assets/` 下載之 6 張教育與 AI 主題高畫質圖片分別整合進封面及 5 大核心挑戰頁面。
- **沉澱專頁與多重視圖更新**：更新 [[synthesis/llm-in-education-challenges]] 納入 Mermaid 拓撲圖譜與 12 頁規格對照清單。

---

## [2026-11-23] query & synthesis | [[synthesis/llm-in-education-challenges|LLM 在教學上的運用問題與防線挑戰]]
- **專題合成與產出**：利用知識庫五篇經典論文，針對「LLM 在教學上的運用問題」進行跨維度橫向合成分析。
- **投影片製作**：生成現代化響應式 HTML 投影片 `slides/llm-in-education-challenges.html`，具備鍵盤翻頁（`←`、`→`、`Space`）、進度條與卡片式風險矩陣。
- **沉澱專頁**：建立 [[synthesis/llm-in-education-challenges]]，包含五大維度深度分析（TruthfulQA 逆向縮放、GCG 越獄攻擊、Beyond Memorization 推論隱私、CAI 說教與閃避、Unlearning 教材版權）與教育應對矩陣。
- **索引更新**：同步登錄於 `index.md` 之 Synthesis 分類。

---

## [2026-11-23] ingest | [[papers/Staab2024-PrivacyInference|Staab et al. (2024) — Beyond Memorization]]
- **下載論文原檔**：`raw/papers/Staab2024-PrivacyInference.pdf` (arXiv:2310.07298, ICLR 2024)。
- **建立論文專頁**：[[papers/Staab2024-PrivacyInference]]，完整收錄推論隱私侵犯威脅模型（$A_1$ 自由文本側寫、$A_2$ 隱藏任務對話刺探）、連續年齡區間對稱重疊度公式、PersonalReddit (PR) 評測成果，以及去識別化與模型對齊失效之實證分析。
- **漣漪式建立關聯詞條**：
  - 任務領域：[[tasks/privacy-protection]] (模型隱私保護)
  - 評測指標：[[benchmarks/personal-reddit]] (PersonalReddit 基準)
- **更新既有知識網絡**：
  - 更新 [[concepts/ai-alignment]]：點出現行安全對齊在隱私維度的嚴重缺位（對個人特徵探測請求拒絕率幾近為 0%）。
  - 更新 [[tasks/machine-unlearning]]：對照「訓練記憶抹除」與「推論時期語意推導」的本質差異。
- **核心突破**：證明大模型帶來的隱私威脅絕非僅限於預訓練記憶外洩，在推論時期大模型具備媲美人類專家的個人側寫能力（GPT-4 達 85.5% Top-1 / 95.2% Top-3），且成本暴降 100 倍、速度提升 240 倍，使得規模化隱私侵犯成為現實。

---

## [2026-11-23] ingest | [[papers/Eldan2023-WhoIsHarryPotter|Eldan & Russinovich (2023) — Who's Harry Potter?]]
- **下載論文原檔**：`raw/papers/Eldan2023-WhoIsHarryPotter.pdf` (arXiv:2310.02238)。
- **建立論文專頁**：[[papers/Eldan2023-WhoIsHarryPotter]]，完整收錄 Approximate Unlearning 演算法、ReLU Logit Offset 公式、1,500 錨點詞典通用置換與通用基準保留（LM Harness）成果。
- **漣漪式建立關聯詞條**：
  - 技術方法：[[methods/approximate-unlearning]] (近似機器遺忘)
  - 任務領域：[[tasks/machine-unlearning]] (機器遺忘與版權合規)
- **更新既有知識網絡**：
  - 更新 [[concepts/ai-alignment]]：將對齊光譜擴充至「事後選擇性記憶抹除（Machine Unlearning）」，補齊對抗侵權與個資外洩之關鍵防禦拼圖。
- **核心突破**：證明在生成式 LLM 中不需耗費 184K GPU-hours 從頭重訓，僅需約 1 GPU-hour 微調即可精準抹除特定長篇版權內容，且幾乎無損常識推理基準。

---

## [2026-11-23] ingest | [[papers/Lin2021-TruthfulQA|Lin et al. (2021) — TruthfulQA]]
- **下載論文原檔**：`raw/papers/Lin2021-TruthfulQA.pdf` (arXiv:2109.07958)。
- **建立論文專頁**：[[papers/Lin2021-TruthfulQA]]，完整收錄 Imitative Falsehoods 定義、Truthfulness 與 Informativeness 雙軸評估機制、多選題 Likelihood 公式與 GPT-judge 自動化評分。
- **漣漪式建立關聯詞條**：
  - 核心概念：[[concepts/inverse-scaling]] (逆向縮放現象)
  - 評測指標：[[benchmarks/truthfulqa]] (TruthfulQA 基準)
  - 任務領域：[[tasks/hallucination-mitigation]] (幻覺抑制與真實性增強)
- **更新既有知識網絡**：
  - 更新 [[concepts/ai-alignment]]：補齊 HHH 架構中的「Honest（誠實/真實）」維度與對抗 Imitative Falsehoods 之關聯。
  - 更新 [[benchmarks/hhh-eval]]：將 TruthfulQA 鏈結為 Honest 維度的代表性評測基準。
- **核心突破**：揭示預訓練模型單純 Scaling Up 無法自動獲得真實性，反會引發更深層的 Inverse Scaling；唯有透過 Post-training 對齊（RLHF/CAI）或檢索增強（WebGPT/RAG）才能打破此困境。

---

## [2026-11-23] ingest | [[papers/Zou2023-UniversalAttacks|Zou et al. (2023) — Universal Adversarial Attacks]]
- **下載論文原檔**：`raw/papers/Zou2023-UniversalAttacks.pdf` (arXiv:2307.15043)。
- **建立論文專頁**：[[papers/Zou2023-UniversalAttacks]]，完整收錄 GCG 演算法數學推導、One-hot 梯度近似、肯定前綴誘導機制與 AdvBench 實驗數據。
- **漣漪式建立關聯詞條**：
  - 技術方法：[[methods/gcg]] (Greedy Coordinate Gradient)
  - 任務領域：[[tasks/adversarial-robustness]], [[tasks/red-teaming]]
  - 評測指標：[[benchmarks/advbench]] (Harmful Strings / Behaviors)
- **更新既有知識網絡**：
  - 更新 [[papers/Bai2022-ConstitutionalAI]]：補充被 GCG 攻擊跨模型轉移突破之安全評估。
  - 更新 [[methods/constitutional-ai]]：補充對抗強健性不足與過擬合風險之挑戰。
  - 更新 [[concepts/ai-alignment]]：加入「經驗對齊 vs. 對抗性對齊」的根本鴻溝討論。
- **核心突破**：證實當前主流的 RLHF 與 Constitutional AI 對齊機制不具備對抗性強健（Aligned $\neq$ Adversarially Aligned），GCG 產生的離散後綴可在多模型間轉移並高機率越獄 ChatGPT、Bard 與 Claude。

---

## [2026-11-23] ingest | [[papers/Bai2022-ConstitutionalAI|Bai et al. (2022) — Constitutional AI]]
- **下載論文原檔**：`raw/papers/Bai2022-ConstitutionalAI.pdf` (arXiv:2212.08073)。
- **建立論文專頁**：[[papers/Bai2022-ConstitutionalAI]]，完整收錄兩階段流程（SL-CAI Critique-Revision、RL-CAI RLAIF）與 Bradley-Terry 偏好損失函數。
- **漣漪式建立關聯詞條**：
  - 技術方法：[[methods/constitutional-ai]], [[methods/rlaif]], [[methods/rlhf]]
  - 任務領域：[[tasks/harmlessness]]
  - 核心概念：[[concepts/ai-alignment]]
  - 評測指標：[[benchmarks/hhh-eval]]
- **核心突破**：利用一套自然語言憲法原則與 CoT 實現 AI Feedback 監督，在完全不依賴人工有害標籤的情況下達成 Helpfulness 與 Harmlessness 的 Pareto 改進，並消除過度閃避（Evasive）回應。

---

## [2026-11-23] init | 知識庫架構與規範初始化
- 建立專用規範檔案 `AGENTS.md`（針對 LLMs & GenAI 領域特化，繁體中文內文與英文技術專有名詞保留）。
- 建立目錄架構：`raw/papers/`, `raw/assets/`, 以及 `wiki/` 轄下 `papers/`, `methods/`, `tasks/`, `benchmarks/`, `concepts/`, `synthesis/`。
- 初始化索引頁面 `index.md` 與活動日誌 `log.md`。
