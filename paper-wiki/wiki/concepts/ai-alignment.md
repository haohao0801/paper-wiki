---
type: concept
name: AI Alignment
aliases: [對齊, 模型對齊, HHH]
tags: [concept, ai-alignment, safety, hhh]
---

# AI Alignment (人工智慧對齊)

## 1. 核心意涵
**AI Alignment** 旨在確保人工智慧系統的行為、目標與輸出，能夠精確契合人類的真實意圖、道德規範與安全界限。

在現代大型語言模型領域，主流業界與學界將對齊目標具體定義為 **HHH 架構 (Helpful, Honest, Harmless)**：
- **Helpful (有幫助)**：準確理解使用者指令，提供實用、切題、高效的協助。
- **Honest (誠實/真實)**：不幻覺（Hallucination）、不捏造事實、不盲目模仿網路人類迷思（參見 [[benchmarks/truthfulqa|TruthfulQA]] 與 [[concepts/inverse-scaling|Inverse Scaling]]），並能準確傳達自身的知識不確定性。
- **Harmless (無害)**：不產生具有危險性、歧視性、惡意違法、推廣暴力或社會偏見的內容。

---

## 2. Helpfulness 與 Harmlessness 的張力 (The HH Tension)

在 [[papers/Bai2022-ConstitutionalAI|Bai et al. (2022)]] 中明確指出：
- 單純追求 **Helpfulness** 的模型，容易成為「對惡意請求百依百順」的幫兇（例如提供製造毒物或駭客攻擊指令）。
- 單純追求 **Harmlessness** 的模型，若採用傳統 [[methods/rlhf|RLHF]] 人工標註，標註員容易偏好「拒絕回答」的回應，導致模型演變成「過度閃避（Evasive）」，甚至拒絕討論正當但敏感的公共議題。
- **解決方案**：透過 [[methods/constitutional-ai|Constitutional AI]]，引導模型學會**正面釐清並解釋反對理由**，在維護無害的同時不損害實用性，達成 Pareto Improvement。

### 經驗對齊 vs. 對抗性對齊 (Empirical vs. Adversarial Alignment)
在 [[papers/Zou2023-UniversalAttacks|Zou et al. (2023)]] 中指出，目前以 SFT/RLHF/CAI 為主的對齊多屬於「經驗對齊」——針對人類正常提問能維持安全邊界，但在遭受演算法最佳化的離散對抗後綴（[[methods/gcg|GCG]]）攻擊時極其脆弱。這意味著現存對齊多為淺層機率遮罩，尚未達成數學或理論上的絕對強健（Adversarially Aligned）。

### 隱私對齊的盲區 (The Privacy Gap in Current Alignment)
在 [[papers/Staab2024-PrivacyInference|Staab et al. (2024)]] 的研究中揭露，現行主流的安全對齊幾乎完全聚焦於「防止有害言論與暴力指示」，卻對**「推論時期隱私侵害（Inference-time Privacy Violation）」**毫無防備。面對探測個人年齡、居住地、收入等非授權個資側寫請求，主流模型（GPT-4、LLaMA-2）的拒絕率甚至為 0%，凸顯現行對齊範式在隱私保護上的嚴重缺位。

---

## 3. 主要對齊技術光譜

```text
預訓練 (Next-Token Prediction)
      │
      ├──> SFT (指令微調, Instruction Tuning)
      │
      ├──> RLHF (人類偏好強化學習: PPO + Reward Model)
      │
      ├──> RLAIF / Constitutional AI (AI 反饋與憲法原則引導)
      │
      ├──> Direct Preference Optimization (DPO, 閉式解無模型對齊)
      │
      └──> Machine Unlearning (事後選擇性記憶抹除 / 近似機器遺忘)
```

---

## 4. 關聯頁面
- 代表文獻：[[papers/Bai2022-ConstitutionalAI|Constitutional AI]], [[papers/Zou2023-UniversalAttacks|Universal Adversarial Attacks]], [[papers/Lin2021-TruthfulQA|TruthfulQA]], [[papers/Eldan2023-WhoIsHarryPotter|Who's Harry Potter?]], [[papers/Staab2024-PrivacyInference|Beyond Memorization]]
- 核心方法：[[methods/constitutional-ai|Constitutional AI]], [[methods/rlaif|RLAIF]], [[methods/rlhf|RLHF]], [[methods/approximate-unlearning|Approximate Unlearning]]
- 關鍵任務：[[tasks/harmlessness|Harmlessness]], [[tasks/red-teaming|Red Teaming]], [[tasks/adversarial-robustness|Adversarial Robustness]], [[tasks/hallucination-mitigation|Hallucination Mitigation]], [[tasks/machine-unlearning|Machine Unlearning]], [[tasks/privacy-protection|Privacy Protection]]
- 評測指標：[[benchmarks/hhh-eval|HHH Evals]], [[benchmarks/advbench|AdvBench]], [[benchmarks/truthfulqa|TruthfulQA]], [[benchmarks/personal-reddit|PersonalReddit]]
