# Research Wiki Index

歡迎來到論文 LLM Wiki 知識庫！本索引頁統整知識庫內所有的論文、核心技術、任務領域、評測指標與橫向綜述。

> [!TIP]
> 若你在 Obsidian 中安裝了 **Dataview** 外掛，底下的動態查詢區塊將會自動依據 YAML Frontmatter 產生即時排序表格。

---

## 📚 論文目錄 (Papers)

```dataview
TABLE year as "年份", authors as "作者", tags as "領域標籤"
FROM "wiki/papers"
SORT year DESC
```

### 論文清單存檔 (Manual Fallback)
| 論文專頁 | 年份 | 第一作者 | 核心突破 / One-line Hook |
| :--- | :--- | :--- | :--- |
| [[papers/Staab2024-PrivacyInference\|Beyond Memorization: Violating Privacy via Inference with Large Language Models]] | 2024 | Robin Staab (ETH Zurich) | 揭示 LLM 推論時期隱私威脅，以 100x 便宜成本精準逆向推論個人私密特徵，現行防禦幾近失效。 |
| [[papers/Eldan2023-WhoIsHarryPotter\|Who's Harry Potter? Approximate Unlearning in LLMs]] | 2023 | Ronen Eldan (Microsoft) | 提出近似機器遺忘框架，僅需 1 GPU-hour 即可抹除特定版權小說記憶且無損通用能力。 |
| [[papers/Zou2023-UniversalAttacks\|Universal and Transferable Adversarial Attacks on Aligned Language Models]] | 2023 | Andy Zou (CMU) | 提出 GCG 演算法，全自動搜尋通用對抗性後綴，實現高成功率的黑箱跨模型越獄攻擊。 |
| [[papers/Bai2022-ConstitutionalAI\|Constitutional AI: Harmlessness from AI Feedback]] | 2022 | Yuntao Bai (Anthropic) | 提出 Constitutional AI 與 RLAIF，以自然語言憲法原則取代人工無害性標註。 |
| [[papers/Lin2021-TruthfulQA\|TruthfulQA: Measuring How Models Mimic Human Falsehoods]] | 2021 | Stephanie Lin (Oxford) | 提出 TruthfulQA 基準，揭露模型規模擴大反而更傾向模仿人類迷思之 Inverse Scaling 現象。 |

---

## ⚙️ 核心技術與方法 (Methods)

```dataview
LIST
FROM "wiki/methods"
SORT file.name ASC
```

### 方法快速索引
- [[methods/approximate-unlearning|Approximate Unlearning]] — 結合強化引導 Logit 截斷與錨點通用標籤之輕量級模型遺忘技術。
- [[methods/gcg|Greedy Coordinate Gradient (GCG)]] — 結合 Top-k 負梯度候選與批次前向評估的離散對抗攻擊演算法。
- [[methods/constitutional-ai|Constitutional AI (CAI)]] — 透過憲法原則引導自我批判與修改的對齊技術。
- [[methods/rlaif|RLAIF]] — 利用語言模型作為 Feedback Model 生成偏好數據並以 RL 訓練。
- [[methods/rlhf|RLHF]] — 傳統人類偏好強化學習框架（SFT + PM + PPO）。

---

## 🎯 任務領域與應用 (Tasks)

```dataview
LIST
FROM "wiki/tasks"
SORT file.name ASC
```

### 任務快速索引
- [[tasks/privacy-protection|Privacy Protection]] — 模型隱私保護，涵蓋訓練記憶洩漏與推論時期惡意側寫防禦。
- [[tasks/machine-unlearning|Machine Unlearning]] — 模型機器遺忘，處理版權合規、GDPR 被遺忘權與高危知識消除。
- [[tasks/hallucination-mitigation|Hallucination Mitigation]] — 模型幻覺抑制與真實性增強任務。
- [[tasks/adversarial-robustness|Adversarial Robustness]] — 語言模型對抗強健性，探討經驗對齊與對抗性對齊之鴻溝。
- [[tasks/red-teaming|Red Teaming]] — 主動探尋模型安全漏洞的人工與自動化紅隊測試。
- [[tasks/harmlessness|Harmlessness]] — 模型安全與無害性任務，著重解決 Evasiveness 矛盾。

---

## 📊 評測基準與數據集 (Benchmarks)

```dataview
TABLE metrics as "核心指標", saturation as "評測狀態"
FROM "wiki/benchmarks"
SORT file.name ASC
```

### 評測快速索引
- [[benchmarks/personal-reddit|PersonalReddit]] — 評估 LLM 推論個人私密特徵（8 大屬性）的真實世界匿名論壇基準。
- [[benchmarks/truthfulqa|TruthfulQA]] — 衡量語言模型真實性與人類常見迷思模仿度之 817 題基準。
- [[benchmarks/advbench|AdvBench]] — 衡量對抗越獄與安全防禦的 1,000 條違規測試集（Harmful Strings / Behaviors）。
- [[benchmarks/hhh-eval|HHH Evals]] — Helpful, Honest, Harmless 二元偏好比較評測基準。

---

## 💡 理論與基礎概念 (Concepts)

```dataview
LIST
FROM "wiki/concepts"
SORT file.name ASC
```

### 概念快速索引
- [[concepts/inverse-scaling|Inverse Scaling]] — 模型參數量擴增反而導致特定任務表現逆向衰退之反常現象。
- [[concepts/ai-alignment|AI Alignment]] — 模型對齊理論、HHH 準則、經驗對齊 vs. 對抗性對齊、機器遺忘光譜、隱私對齊盲區。

---

## 🔬 專題綜述與橫向對比 (Synthesis)

```dataview
LIST
FROM "wiki/synthesis"
SORT file.mtime DESC
```

### 專題對比成果
- [[synthesis/llm-in-education-challenges|LLM 在教學上的運用問題與防線挑戰]] — 跨文獻橫向整合 TruthfulQA、GCG、推論隱私、CAI 與機器遺忘之教育落地風險分析矩陣（附 [互動式 HTML 簡報投影片](file:///C:/Users/User/.gemini/antigravity/scratch/paper-wiki/slides/llm-in-education-challenges.html)）。
