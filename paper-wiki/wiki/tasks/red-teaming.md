---
type: task
name: Red Teaming
aliases: [紅隊演練, 紅隊測試, Automated Red Teaming]
tags: [task, safety, evaluation, red-teaming]
---

# Red Teaming (紅隊演練)

## 1. 任務定義
**Red Teaming (紅隊演練)** 是一種主動尋找 AI 系統脆弱點、潛在偏見、邏輯盲區與安全防線漏洞的對抗性測試流程。

在 LLM 安全生命週期中，紅隊測試通常分為兩種範式：
1. **人工紅隊 (Human Red Teaming)**：招募安全專家或群眾標註員，嘗試透過各種日常誘騙、邏輯陷阱與話術引誘模型產生有害輸出（如 [[papers/Bai2022-ConstitutionalAI|Bai et al., 2022]] 所採用的方式）。
2. **自動化紅隊 (Automated Red Teaming)**：
   - 利用輔助語言模型自動產生攻擊提示詞（Perez et al., 2022）。
   - 利用離散梯度最佳化自動挖掘致命弱點（如 [[methods/gcg|GCG]] 演算法，見 [[papers/Zou2023-UniversalAttacks|Zou et al., 2023]]）。

---

## 2. 演進與挑戰
- 早期的人工紅隊演練成本極高且難以窮舉邊界情況。
- 透過自動化紅隊演練發現的對抗樣本，能回流為 [[methods/constitutional-ai|Constitutional AI]] 的 Critique-Revision 訓練素材，形成攻防演進閉環。

---

## 3. 關聯主題
- 相關攻擊研究：[[papers/Zou2023-UniversalAttacks|Zou et al. (2023)]]
- 相關防禦技術：[[methods/constitutional-ai|Constitutional AI]], [[methods/rlhf|RLHF]]
- 相關任務：[[tasks/adversarial-robustness|Adversarial Robustness]], [[tasks/harmlessness|Harmlessness]]
