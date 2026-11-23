---
type: method
name: Reinforcement Learning from AI Feedback
aliases: [RLAIF, AI Feedback RL]
tags: [rl, rlaif, ai-alignment, preference-learning]
---

# Reinforcement Learning from AI Feedback (RLAIF)

## 1. 核心定義與直覺 (Intuition)
**RLAIF (Reinforcement Learning from AI Feedback)** 是一種利用語言模型（Feedback Model）自主生成偏好標籤（Preference Labels），進而訓練 Reward/Preference Model 並進行強化學習對齊的技術。

傳統 [[methods/rlhf|RLHF]] 的核心瓶頸在於需要大量人類比較資料 $(x, y_w, y_l)$。RLAIF 的核心假設是：**隨著語言模型參數量與推理能力增長（特別是結合 Chain-of-Thought），大模型對優劣回應的評估能力已可比擬甚至超越一般群眾標註員（Crowdworkers）**。

---

## 2. 演算法運作機制

```text
Prompt x ──> 策略模型生成 (y_A, y_B)
                    │
                    ▼
Feedback Model (結合 CoT 推理 + 判斷原則)
                    │
                    ▼
AI Preference Target: P(A ≻ B)  ──>  [Clamp 0.4~0.6]
                    │
                    ▼
訓練偏好模型 (PM): 最小化 Bradley-Terry Loss
                    │
                    ▼
PPO 微調策略模型 (以 PM 作為 Reward Signal)
```

### 關鍵技術要點
1. **多選題評估格式 (Multiple Choice Formulation)**：
   將偏好評估轉為選擇題，直接讀取 Token `(A)` 與 `(B)` 的 Log-probabilities，產生平滑的 Soft Target 分佈。
2. **Chain-of-Thought (CoT) 增強**：
   引入「Let's think step-by-step」，強制模型先輸出推理鏈再給出勝負結論，顯著提升評估的一致性與準確度。
3. **機率截斷 (Probability Clamping)**：
   CoT 評估往往極度自信（機率接近 0 或 1），容易導致 PM 過擬合。將 AI 偏好目標截斷於 $[0.40, 0.60]$ 區間內能大幅穩定強化學習過程。

---

## 3. 代表性論文與演進

- **2022-12** [[papers/Bai2022-ConstitutionalAI|Bai et al. (2022)]]：在 Constitutional AI 中率先實作 RLAIF，證明完全無需人類有害性標註即可超越傳統 HH RLHF。
- **2023** Google 發表《RLAIF: Scaling Reinforcement Learning from Human Feedback with AI Feedback》(Lee et al., 2023)，系統性證明在摘要、對話等一般任務上 RLAIF 達到與 RLHF 相同的勝率。

---

## 4. RLAIF vs. RLHF 比較

| 維度 | RLHF | RLAIF |
| :--- | :--- | :--- |
| **標註來源** | 人工標註員 (Crowdworkers) | 獨立評估模型 (Feedback Model) |
| **標註成本與速度** | 昂貴、耗時長 (數週至數月) | 極快、近乎邊際成本為零 |
| **標註一致性** | 存在個體偏見、噪聲大 | 嚴格依循 Prompt/原則，具高度一致性 |
| **透明度** | 低（隱性偏好分佈） | 高（可提供完整 CoT 推理審查） |
| **主要風險** | 容易獎勵閃避式回答 (Evasiveness) | 容易誘發 Goodharting、受限於模型自身認知盲點 |

---

## 5. 關聯主題
- 基礎框架：[[methods/rlhf|RLHF]]
- 代表應用：[[methods/constitutional-ai|Constitutional AI]]
- 核心目標：[[concepts/ai-alignment|AI Alignment]]
- 評測指標：[[benchmarks/hhh-eval|HHH Evals]]
