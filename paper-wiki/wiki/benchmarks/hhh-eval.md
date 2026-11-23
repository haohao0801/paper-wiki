---
type: benchmark
name: HHH Evals
aliases: [HHH Benchmark, Helpful Honest Harmless Evaluations]
tags: [benchmark, evaluation, alignment, hhh]
metrics: [Binary Comparison Accuracy, Elo Rating]
saturation: "Active / Evolving"
---

# HHH Evals (Helpful, Honest, Harmless Evaluations)

## 1. 評測目標與形式
**HHH Evals** 是由 Anthropic (Askell et al., 2021; Bai et al., 2022) 提出的一系列評測基準，專門衡量語言模型在 Helpful（有幫助）、Honest（誠實）與 Harmless（無害）三個對齊維度上的能力。

### 評測形式
- **二元比較選擇題 (Binary Comparison Questions)**：
  提供一段人類與助理的對話，最後附上兩個不同模型生成的候選回應 $(A)$ 與 $(B)$。
- 模型需透過計算 Normalized Log-probabilities 預測哪一個選項更符合 HHH 原則。
- 在 [[papers/Bai2022-ConstitutionalAI|Bai et al. (2022)]] 中，Anthropic 擴充了 217 道高難度比較題目，特別著重於：
  - **細微的無害性判斷**（Subtle tests of harmlessness）。
  - **懲罰閃避式回覆 (Penalizing Evasive Responses)**：若兩個選項皆無害，偏好能提供深入思維與解釋的選項，而非單純回絕的選項。

---

## 2. 代表性表現基準 (SOTA Snapshots)

- **預訓練基礎模型 (52B)**：二元比較準確率約 50%~60%（接近隨機猜測或微幅優於隨機）。
- **預訓練模型 + Chain-of-Thought (CoT)**：準確率顯著攀升至 70%~75% 以上。
- **人類標註偏好模型 (HH PM from Human Feedback)**：準確率約 75%~80%。
- **結論**：在大模型規模（>52B）下，搭配 CoT 的 AI 評估能力已具備匹敵人類群眾標註員的水準。

---

## 3. 關聯頁面
- 核心文獻：[[papers/Bai2022-ConstitutionalAI|Constitutional AI: Harmlessness from AI Feedback]]
- 評測技術：[[methods/rlaif|RLAIF]]
- 相關概念：[[concepts/ai-alignment|AI Alignment]]
- 誠實性基準：[[benchmarks/truthfulqa|TruthfulQA]]（專門針對 HHH 中 "Honest" 維度的代表性評測）
