---
type: method
name: Reinforcement Learning from Human Feedback
aliases: [RLHF]
tags: [rl, rlhf, ai-alignment, preference-learning]
---

# Reinforcement Learning from Human Feedback (RLHF)

## 1. 核心定義與直覺 (Intuition)
**RLHF (Reinforcement Learning from Human Feedback)** 是一種利用人類反饋資料優化語言模型行為的對齊技術。它解決了傳統 Next-Token Prediction 預訓練目標與人類實際使用意圖（Helpful, Honest, Harmless）之間的根本脫節（Misalignment）。

---

## 2. 三階段標準流程

1. **監督式微調 (Supervised Fine-Tuning, SFT)**：
   在高品質的人類問答展示資料（Demonstrations）上微調預訓練模型。
2. **訓練獎勵/偏好模型 (Reward Model / Preference Model, RM/PM)**：
   採樣模型生成的一對或多個回應，由人類標註員排列優劣次序，並依據 **Bradley-Terry 模型** 最小化 Cross-Entropy 損失：
   $$ \mathcal{L}_{\text{RM}}(\theta) = - \mathbb{E}_{(x, y_w, y_l) \sim \mathcal{D}} \left[ \log \sigma \left( r_\theta(x, y_w) - r_\theta(x, y_l) \right) \right] $$
3. **強化學習微調 (RL Fine-Tuning via PPO)**：
   以 SFT 模型作為初始策略 $\pi_\phi$，使用 PPO 演算法極大化 RM 給出的獎勵，同時加入 KL Divergence 懲罰項以避免模型策略過度偏離參考模型（Policy Drift）：
   $$ \text{obj}(\phi) = \mathbb{E}_{(x, y) \sim \mathcal{D}_{\pi_\phi}} \left[ r_\theta(x, y) - \beta \, \mathbb{D}_{\text{KL}}\left(\pi_\phi(y|x) \parallel \pi_{\text{SFT}}(y|x)\right) \right] $$

---

## 3. 演進脈絡與衍生變體

- **2017** Christiano et al. 奠定人類偏好強化學習理論。
- **2022** OpenAI 發表 InstructGPT (Ouyang et al., 2022)，確立現代 LLM 對齊基本範式。
- **2022-12** [[papers/Bai2022-ConstitutionalAI|Bai et al. (2022)]] 指出傳統 RLHF 在處理 Harmlessness 時容易陷入過度閃避（Evasiveness），並提出以 [[methods/rlaif|RLAIF]] 與 [[methods/constitutional-ai|Constitutional AI]] 取代人工標籤。
- **2023** Rafailov et al. 提出 [[methods/dpo|DPO (Direct Preference Optimization)]]，推導出隱式 Reward，完全跳過 RL 演算法。

---

## 4. 關聯主題
- 延伸技術：[[methods/rlaif|RLAIF]], [[methods/constitutional-ai|Constitutional AI]]
- 核心目標：[[concepts/ai-alignment|AI Alignment]]
- 相關任務：[[tasks/harmlessness|Harmlessness]]
