---
type: benchmark
name: TruthfulQA
aliases: [TruthfulQA Benchmark]
tags: [benchmark, evaluation, truthfulness, hallucination, ai-alignment]
metrics: [% True, % True + Info, MC1/MC2 Accuracy]
saturation: "Challenging / Active"
---

# TruthfulQA

## 1. 評測目標與核心特質
**TruthfulQA** 是由 Oxford 與 OpenAI 研究團隊於 2021 年在 [[papers/Lin2021-TruthfulQA|Lin et al. (2021)]] 中提出的基準測試，專門檢驗語言模型在回答問題時能否堅持**真實性（Truthfulness）**，避免模仿人類在網路上流傳的迷思、偽科學、陰謀論與偏見。

### 核心特點
- **題庫規模**：817 道題目，涵蓋 38 個多元類別（健康、法律、金融、社會學等）。
- **目標鎖定 Imitative Falsehoods**：專門挑選「人類常答錯、網路文本中充斥錯誤答案」的問題。
- **首次揭露 [[concepts/inverse-scaling|Inverse Scaling]]**：未經對齊的純預訓練模型隨著參數擴增，分數反而單調遞減。

---

## 2. 評測維度與評估指標

TruthfulQA 強調回答不能只看真實性，更必須兼顧資訊量：
- **`% True`**：回答內容符合客觀事實的比例（注意：回答「無可奉告」在定義上也算 True）。
- **`% Info`**：回答具備實質資訊量、有助於降低問題不確定性的比例。
- **`% True + Info` (黃金指標)**：既真實又有實用資訊的回應比例。
- **MC1 / MC2 多選題指標**：
  - **MC1 (Single-true)**：在單一正確答案與多個錯誤選項中，正確選項的 Likelihood 排名第一的機率。
  - **MC2 (Multi-true)**：計算所有正確選項集合的 Normalized Total Probability。

---

## 3. 代表模型歷史得分比較

| 模型 | % True | % Info | % True + Info | 備註 |
| :--- | :--- | :--- | :--- | :--- |
| **人類受試者基準** | **94%** | 93% | **87%** | 專家查證基準 |
| **GPT-3-175B (Base)** | 20.4% | **97.6%** | 18.2% | 純預訓練大模型極易受騙 |
| **GPT-Neo/J-6B** | 26.8% | 90.0% | 18.2% | 展現逆向縮放現象 |
| **InstructGPT-175B** | 43.8% | 85.0% | 31.0% | RLHF 對齊大幅改善真實性 |
| **WebGPT-175B** | **74.5%** | 82.0% | **54.0%** | 搭配網路搜尋引擎查證之模型 |

---

## 4. 關聯主題
- 提出論文：[[papers/Lin2021-TruthfulQA|Lin et al. (2021)]]
- 相關現象：[[concepts/inverse-scaling|Inverse Scaling]]
- 對齊維度：[[concepts/ai-alignment|AI Alignment (Honest Pillar)]], [[benchmarks/hhh-eval|HHH Evals]]
- 相關任務：[[tasks/hallucination-mitigation|Hallucination Mitigation]]
