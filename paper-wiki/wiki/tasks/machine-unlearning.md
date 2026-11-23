---
type: task
name: Machine Unlearning
aliases: [機器遺忘, 模型遺忘, Right to be Forgotten, 選擇性遺忘]
tags: [task, safety, privacy, copyright, alignment]
---

# Machine Unlearning (大型語言模型機器遺忘)

## 1. 任務定義與時代背景
**Machine Unlearning (機器遺忘)** 旨在讓預訓練完畢的機器學習模型在不影響通用語言與推理能力的前提下，**精確清除或抹除特定子集數據（如個資、侵權書籍、危險武器化知識）的記憶**。

### 促成遺忘任務爆發的三大推力：
1. **版權法律合規 (Copyright Compliance)**：出版商與創作者對未授權爬取書籍、新聞提起大規模侵權訴訟。
2. **個人隱私法規 (GDPR Right to be Forgotten)**：要求系統必須依用戶請求撤銷並刪除其個人數據（PII）。
3. **極端安全對齊 (Dual-use & CBRN Removal)**：生物化學武器（CBRN）與進階網路攻擊等高危知識的徹底消除。

---

## 2. 核心技術挑戰
- **災難性遺忘反向版 (Catastrophic Collateral Damage)**：嘗試遺忘特定名詞，往往連帶損害相鄰的基礎語意結構。
- **潛在記憶殘留與逆向探測 (Residual Knowledge & Adversarial Probing)**：模型表面上不輸出，但藉由 [[methods/gcg|GCG 對抗後綴]] 或機率分佈擾動，隱藏記憶可能再度被激發。
- **非虛構文本（Non-fiction）的遺忘困難**：小說有獨特專有名詞易於錨定；教科書與歷史事實與世界知識高度交織，切割極為困難。
- **訓練記憶消除 vs. 推論時期推導 (Memorization vs. Inference Privacy)**：
  在 [[papers/Staab2024-PrivacyInference|Staab et al. (2024)]] 中指出，機器遺忘只能清除模型權重中「已記住」的數據；但只要模型保留通用的語言理解與世界推理能力，它仍能在推論時期從使用者提供的新文本中推導出高度私密的個人屬性（如居住地、收入、年齡），顯示隱私保護不能僅仰賴機器遺忘。

---

## 3. 代表性研究與里程碑
- **2023** [[papers/Eldan2023-WhoIsHarryPotter|Eldan et al. (2023)]]：發表首個在生成式 7B 模型上成功抹除《哈利波特》小說的實踐，開創 [[methods/approximate-unlearning|Approximate Unlearning]] 範式。

---

## 4. 關聯主題
- 核心技術：[[methods/approximate-unlearning|Approximate Unlearning]]
- 相關研究：[[papers/Eldan2023-WhoIsHarryPotter|Who's Harry Potter?]]
- 對抗風險：[[tasks/adversarial-robustness|Adversarial Robustness]]
- 整體理論：[[concepts/ai-alignment|AI Alignment]]
