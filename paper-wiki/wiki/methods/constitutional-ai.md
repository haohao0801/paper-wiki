---
type: method
name: Constitutional AI
aliases: [CAI, 憲法 AI]
tags: [ai-alignment, safety, rlaif, sft]
---

# Constitutional AI (CAI)

## 1. 核心定義與直覺 (Intuition)
**Constitutional AI (CAI)** 是一種使大語言模型能夠藉助**自然語言原則（憲法，Constitution）**進行自我監督與對齊的技術範式，由 Anthropic 於 2022 年在 [[papers/Bai2022-ConstitutionalAI|Bai et al. (2022)]] 中正式提出。

其核心思想在於：**以明確、高透明度的原則取代黑盒且龐大的人工標註數據**。人類監督者僅需制定十餘條規則（例如「請選擇更誠實、友善且不鼓勵違法行為的回應」），模型即能以此作為準則，對自身生成的內容進行批判（Critique）、修改（Revision）並產生偏好標籤（AI Feedback）。

---

## 2. 核心架構與兩階段流程

CAI 通常由兩個互補階段組成：

```text
Prompt ──> 初始有害生成 ──> [Critique] ──> [Revision] ──> SFT 微調 (SL-CAI)
                                                               │
                                                               ▼
RL-CAI (RLAIF) <── PPO 更新 <── 偏好模型 (PM) <── AI 偏好標註 (Feedback Model)
```

1. **SL 階段 (Critique $\to$ Revision $\to$ SFT)**：
   - 透過 Few-shot 提示詞激發模型按照特定憲法條款進行自我批判與重寫，改變模型的輸出分佈，使其落入無害區域（On-distribution）。
2. **RL 階段 (RLAIF)**：
   - 使用 Feedback Model 評估候選回應對，構建 AI Preference Dataset，訓練 Preference Model (PM) 並透過 PPO 強化學習進行策略微調。

---

## 3. 代表性論文演進時間軸 (Evolution Timeline)

- **2022-12** [[papers/Bai2022-ConstitutionalAI|Bai et al. (2022)]]：正式發表 Constitutional AI，利用 16 條原則成功在無人類無害標籤下訓練出非閃避式（Non-evasive）的 Harmless Assistant。
- **2023** Anthropic 發表其正式的公開版 Claude Constitution，將條款擴展涵蓋聯合國人權宣言、資料科學價值觀等。

---

## 4. 優勢與權衡 (Trade-offs)

### 優勢
- **極高擴展性 (Scalable Oversight)**：擺脫對昂貴人工毒性標註的依賴，大幅加速實驗迭代週期。
- **解決 Evasiveness 矛盾**：能訓練出願意解釋「為什麼這是有害的」而非僅回覆「我無法回答」的健全助理。
- **規則透明可解釋**：治理原則以自然語言寫成，便於審查與動態增刪。

### 局限與挑戰
- **Goodharting 與說教語氣 (Preachiness)**：過度訓練時容易誘發冗長的道德說教。
- **基礎模型能力門檻**：自我批判與 AI 反饋高度依賴 Feedback Model 本身強大的語言理解與推理能力。
- **對抗強健性不足 (Adversarial Vulnerability)**：在 [[papers/Zou2023-UniversalAttacks|Zou et al. (2023)]] 的研究中證實，即便經過 CAI 嚴格訓練的 Claude 系列，面對全自動離散梯度攻擊（如 [[methods/gcg|GCG]]）與誘導提示時，仍可能被成功越獄（Jailbreak），顯示經驗對齊與對抗性強健（Adversarially Aligned）仍存在顯著鴻溝。

---

## 5. 關聯主題
- 前身技術：[[methods/rlhf|RLHF]]
- 核心實踐：[[methods/rlaif|RLAIF]]
- 基礎概念：[[concepts/ai-alignment|AI Alignment]]
- 關鍵任務：[[tasks/harmlessness|Harmlessness]], [[tasks/red-teaming|Red Teaming]]
