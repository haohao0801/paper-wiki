# AGENTS.md — 論文 LLM Wiki 知識庫維護規範

這是一份針對 **大語言模型與生成式 AI（LLMs & Generative AI）** 學術論文知識庫的專屬維護規範。
本知識庫設計為常駐累積型（Compounding Knowledge Base），並完全適配 **Obsidian** 瀏覽與圖譜檢視。

---

## 1. 核心維護哲學與語言規範

1. **語言與用語規範**：
   - **內文撰寫**：一律使用 **繁體中文（台灣習慣用語）** 撰寫說明與分析（如：資訊、推論、模型、最佳化、記憶體）。
   - **專有名詞保留**：關鍵技術術語、模型名稱、評測指標、研究方法與論文原名 **強制保留英文原文**，切勿生硬翻譯。
     - *正確範例*：Self-Attention, In-context Learning, Few-shot, Ablation Study, Loss Function, Alignment, Reward Model, Perplexity, Throughput, Latency。
     - *避免使用*：自注意力（不推薦，使用 Self-Attention）、消融實驗（使用 Ablation Study）。
2. **數學公式與演算法**：
   - 關鍵數學推導、Objective Function、Loss Function 與演算法步驟，**必須保留完整標準 LaTeX 語法**（行內使用 `$math$`，獨立區塊使用 `$$math$$`）。
   - 若論文演算法有關鍵創新步驟，必須提供清晰的 Algorithm 虛擬碼或核心數學推導。
3. **知識複利累積（Compounding Wiki）**：
   - 拒絕單純的 RAG 碎片化問答。每篇論文吸收後，必須將核心觀點與方法編譯進 Wiki 網絡，主動關聯既有文獻，標註繼承、改良、超越或矛盾。
4. **客觀批判視角**：
   - 嚴格區分「作者宣稱（Authors' Claims）」與「客觀實驗結果（Empirical Evidence）」。
   - 必須記錄 Ablation Study 結論、計算硬體資源限制、Baseline 公平性以及潛在失效情況（Failure Modes）。

---

## 2. 原始文獻管理規範（Raw Sources Layer）

`raw/` 目錄為**唯讀層（Immutable Sources）**，Agent 絕不可直接修改原始檔案。

1. **論文輸入與下載**：
   - **對話中提供 PDF**：將 PDF 儲存至 `raw/papers/<AuthorYYYY-Topic>.pdf`。
   - **提供 ArXiv 或網址連結**：Agent 主動使用工具下載對應的 PDF 原檔，儲存至 `raw/papers/<AuthorYYYY-Topic>.pdf`。
   - **論文命名範例**：`Vaswani2017-Transformer.pdf`, `Rafailov2023-DPO.pdf`, `Dao2022-FlashAttention.pdf`。
2. **圖表與資產**：
   - 論文的關鍵架構圖、流程圖若截圖或提取，存放在 `raw/assets/`，檔名格式為 `<AuthorYYYY-Topic>-fig1.png`。

---

## 3. 目錄結構與檔案命名規範

```text
paper-wiki/
├── AGENTS.md                  # 本操作規範
├── index.md                   # 知識庫全覽索引（Obsidian Dataview + 分類導航）
├── log.md                     # 時間序列操作記錄（Append-only）
│
├── raw/                       # 【唯讀原始文獻】
│   ├── papers/                # 存放 PDF 原檔（AuthorYYYY-Topic.pdf）
│   └── assets/                # 關鍵圖表截圖（AuthorYYYY-Topic-figX.png）
│
└── wiki/                      # 【LLM 編譯維護層，全面支援 [[Wikilinks]]】
    ├── papers/                # 單篇論文詳細頁面（格式：AuthorYYYY-Topic.md）
    ├── methods/               # 架構/技術/演算法（格式：kebab-case，如 lora.md, dpo.md）
    ├── tasks/                 # 任務與應用領域（如 reasoning.md, code-generation.md）
    ├── benchmarks/            # 數據集與評測標準（如 gsm8k.md, mmlu-pro.md）
    ├── concepts/              # 核心理論與機制（如 scaling-laws.md, kv-cache.md）
    └── synthesis/             # 橫向對比、領域 Survey、專題探討總結
```

---

## 4. 頁面範本與規範（Page Templates）

### A. 論文專頁範本：`wiki/papers/AuthorYYYY-Topic.md`
```markdown
---
type: paper
title: "Paper Full English Title"
authors: [Author One, Author Two]
year: YYYY
arxiv: "https://arxiv.org/abs/xxxx.xxxxx"
code: "https://github.com/..."
tags: [llm, alignment, rlhf]
date_added: YYYY-MM-DD
---

# Paper Full English Title

- **一言以蔽之 (One-line Hook)**：一句話點出該論文提出何種全新機制或核心突破。
- **關聯頁面 (Wiki Links)**：[[methods/...]], [[tasks/...]], [[benchmarks/...]], [[concepts/...]]
- **原始文檔**：`raw/papers/AuthorYYYY-Topic.pdf`

## 1. 研究背景與核心痛點 (Problem & Motivation)
- 前人方法有何缺陷或效能瓶頸？
- 為何現有 Baselines 無法滿足需求？

## 2. 核心方法與技術創新 (Methodology & Technical Innovation)
- 創新架構與運作機制解構。
- **關鍵數學推導與 Loss Function**：
  $$ \mathcal{L}_{example} = \mathbb{E} [ ... ] $$
- 演算法虛擬碼或核心流程步驟。

## 3. 實驗設計與關鍵成果 (Experiments & Empirical Results)
- **評測基準 (Benchmarks)**：[[benchmarks/...]]
- **主要 Baseline 對照組**：
- **主要成果與關鍵數值**：列出最核心的數據提升（如 Benchmark 分數、Throughput、Memory 降幅）。
- **關鍵 Ablation Study 結論**：哪些組件真正發揮作用？

## 4. 局限性與批判性討論 (Limitations & Discussion)
- 計算成本、顯存限制、未覆蓋的 Edge Cases、推論 Latency 或評測公平性爭議。

## 5. 文獻脈絡關聯 (Connections & Lineage)
- **繼承自 (Builds on)**：[[papers/...]], [[methods/...]]
- **對比與競爭 (Alternatives)**：[[papers/...]], [[methods/...]]
- **後續改進 / 超越 (Extended / Superseded by)**：[[papers/...]]
```

### B. 技術方法範本：`wiki/methods/<method-name>.md`
- **核心定義與直覺 (Intuition)**
- **數學表述 / 機制圖解**
- **代表性論文演進時間軸 (Evolution Timeline)**：按時間記錄各篇引入、改良或評測此方法的論文 `[[papers/AuthorYYYY-Topic]]`。
- **優缺點與適用場景 (Trade-offs)**

### C. 評測基準範本：`wiki/benchmarks/<benchmark-name>.md`
- **評測目標與評估指標 (Metrics)**：如 Pass@1, Accuracy, Win Rate。
- **已知問題與偏誤 (Biases & Saturation)**：例如資料污染（Data Contamination）、評測飽和度。
- **代表模型表現歷史 (SOTA Snapshots)**

---

## 5. 全自動匯入流水線（Autonomous Ingestion Pipeline）

當使用者提供 ArXiv 連結、論文 PDF 或指示解析論文時，Agent 必須**全自動**依序執行以下 5 個步驟：

1. **取得文獻**：
   - 若為網址/ArXiv，使用工具下載 PDF 至 `raw/papers/AuthorYYYY-Topic.pdf`。
   - 提取論文 Title, Authors, Year, Abstract, Key Equations, Baselines, Experiments, Limitations。
2. **建立單篇論文頁**：
   - 建立 `wiki/papers/AuthorYYYY-Topic.md`，填入標準結構，特別確保關鍵數學推導與 Loss Function 保留 LaTeX 原式。
3. **漣漪式更新（Ripple Update - 知識庫核心步驟）**：
   - 識別該論文涉及的 3~8 個實體：
     - **新方法/概念**：自動在 `wiki/methods/` 或 `wiki/concepts/` 建立新頁面。
     - **既有頁面**：更新對應的 `methods/`、`tasks/`、`benchmarks/` 頁面，將新論文的實驗結論、變體或 SOTA 數據追加進演進時間軸。
     - **矛盾與質疑檢驗**：若本篇論文質疑或超越了先前的文獻，必須在兩篇論文與對應方法頁中互加交叉引註（Cross-reference）。
4. **更新索引與時間軸日誌**：
   - **`index.md`**：將新論文與新建立的詞條歸入對應分類清單。
   - **`log.md`**：在最上方（或最末端）追加標準紀錄：
     ```markdown
     ## [YYYY-MM-DD] ingest | [[papers/AuthorYYYY-Topic|Author et al. (YYYY)]]
     - 建立了論文專頁。
     - 漣漪式更新/建立：[[methods/...]], [[tasks/...]], [[benchmarks/...]]
     - 核心突破：一句話總結核心突破。
     ```
5. **輸出執筆報告**：
   - 完成所有檔案寫入後，向使用者輸出簡明摘要：
     - 📌 **論文核心亮點**：2~3 句話摘要關鍵貢獻與技術創新。
     - 🔄 **更動檔案清單**：列出本次新建與更新的所有 Wiki 檔案。
     - 💡 **知識庫脈絡連結**：說明本篇論文如何加深或挑戰知識庫現有文獻。

---

## 6. 查詢與知識沉澱規範（Query & Compound Protocol）

當使用者提出綜合性研究問題（如：「請幫我比較 DPO、PPO 與 KTO 在顯存與訓練穩定度上的差異」）：
1. Agent 檢索 `index.md` 與相關的 `wiki/papers/`、`wiki/methods/` 檔案。
2. 進行跨文獻合成與分析，回答中使用標準 `[[Wikilinks]]`。
3. **知識沉澱（Compound Back）**：
   - 若該回答包含具備長期參考價值的橫向對比表、綜述或架構選型指南，**主動將其編譯為新檔案** `wiki/synthesis/<topic-slug>.md`。
   - 同步更新 `index.md` 與 `log.md`，使探索過程直接轉化為永久資產。

---

## 7. 知識庫健檢規範（Lint Protocol）

當使用者指示「健檢」或定期維護時，檢查：
1. **孤島頁面（Orphans）**：檢測沒有任何其他頁面入鏈（Incoming Wikilinks）的檔案。
2. **未實體化術語**：論文內文多次提及但尚未在 `methods/` 或 `benchmarks/` 建立專屬頁面的熱門技術。
3. **過時宣稱（Stale Claims）**：檢查早期論文聲稱 SOTA 但已被後續收錄論文超越的陳述，標記更新。
