---
type: task
name: Adversarial Robustness
aliases: [對抗強健性, 模型抗攻擊性, Jailbreak Robustness]
tags: [task, safety, adversarial-attack, robustness]
---

# Adversarial Robustness (語言模型對抗強健性)

## 1. 任務定義與問題本質
**Adversarial Robustness (對抗強健性)** 衡量語言模型在遭遇惡意構造的擾動輸入（例如對抗性後綴、字元置換、編碼混淆或提示詞越獄）時，依然能夠堅持其安全邊界與對齊原則的能力。

在 [[papers/Zou2023-UniversalAttacks|Zou et al. (2023)]] 發表後，學界深刻體認到：
**「一般的經驗對齊（Empirical Alignment via SFT/RLHF）並不等同於具備對抗強健性（Adversarial Alignment）。」**

---

## 2. 核心攻擊光譜
1. **人工越獄提示詞 (Manual Jailbreaks)**：如「DAN (Do Anything Now)」、虛構小說角色扮演。缺點是脆弱且容易被特定關鍵字攔截。
2. **自動離散梯度攻擊 (Automated Discrete Gradient Attacks)**：
   - 代表方法：[[methods/gcg|Greedy Coordinate Gradient (GCG)]]、AutoPrompt。
   - 特色：無需人類技巧，全自動利用模型白箱梯度算出通用、可轉移的後綴字串。
3. **黑箱多輪誘導 (Multi-turn Jailbreak)**：利用多輪對話逐步弱化模型的警覺防線。

---

## 3. 防禦手段與面臨挑戰
- **輸入困惑度過濾 (Perplexity / SmoothLLM)**：過濾語義混亂的高 PPL Token，但容易被經過自然語義約束的對抗樣本繞過。
- **對抗訓練 (Adversarial Training)**：將對抗後綴動態加入訓練集並標註正確的拒絕回覆。挑戰在於會顯著損害模型在正常基準（Clean Accuracy）上的通用能力。
- **防禦層前置過濾 (Input Guards)**：如 Llama Guard 或內容審查模型，但本質上只是增加了另一層可被攻擊的目標。

---

## 4. 關聯主題
- 經典攻擊研究：[[papers/Zou2023-UniversalAttacks|Zou et al. (2023)]]
- 代表攻擊方法：[[methods/gcg|GCG]]
- 評測資料庫：[[benchmarks/advbench|AdvBench]]
- 安全對齊理論：[[concepts/ai-alignment|AI Alignment]]
