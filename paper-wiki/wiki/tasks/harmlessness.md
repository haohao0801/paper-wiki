---
type: task
name: Harmlessness
aliases: [無害性, 安全對齊, Safety]
tags: [task, safety, harmlessness, red-teaming]
---

# Harmlessness (模型無害性任務)

## 1. 任務定義與範疇
在語言模型對齊領域，**Harmlessness** 任務要求模型在面對可能引發倫理風險、違法行為、心理危害或社會偏見的 Prompt 時，做出符合安全界限的行為反應。

具體防禦範疇包括：
- 違法犯罪輔助（如駭入他人網路、製造危險物品、逃漏稅）
- 歧視、仇恨言論與性別/種族偏見
- 暴力、自殘或未成年人不當內容
- 醫療/法律等高風險領域的不實誇大建言

---

## 2. 核心技術挑戰：Evasiveness vs. Thoughtful Engagement

在 [[papers/Bai2022-ConstitutionalAI|Bai et al. (2022)]] 之前，模型安全主要透過兩種手段達成：
1. **關鍵字/黑名單過濾**：機械式攔截，容易被混淆提示（Jailbreak）繞過。
2. **RLHF 負向強化**：導致模型過度保守，動輒回覆「Sorry, I cannot respond to this content」。

### Constitutional AI 的典範轉移
- **Non-Evasive Harmlessness**：模型不再簡單閉嘴，而是清楚點出該請求為何不道德或違法，並提供建設性、正向的替代方案（例如：詢問如何偷竊食物時，正面拒絕並提供社區食物銀行與社會救助管道）。

---

## 3. 代表性評測與訓練手法
- **測試方式**：[[tasks/red-teaming|Red Teaming]]（紅隊演練，藉由人類或自動化模型主動引誘模型違規）。
- **主流訓練法**：[[methods/constitutional-ai|Constitutional AI]], [[methods/rlaif|RLAIF]], [[methods/rlhf|RLHF]]。
- **評測基準**：[[benchmarks/hhh-eval|HHH Evals]], PALMS, RealToxicityPrompts。
