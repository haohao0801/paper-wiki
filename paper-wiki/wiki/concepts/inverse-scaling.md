---
type: concept
name: Inverse Scaling
aliases: [逆向縮放, 反向擴展, Inverse Scaling Law]
tags: [concept, scaling-laws, evaluation, ai-alignment]
---

# Inverse Scaling (逆向縮放現象)

## 1. 核心概念與直覺
傳統的神經語言模型縮放法則（Scaling Laws，如 Kaplan et al., 2020）指出，隨著參數量（Model Parameters）、計算量（Compute）與訓練資料集增加，模型的交叉熵損失（Cross-Entropy Loss / Perplexity）與下游任務表現會呈現冪律（Power-law）進步。

然而，**Inverse Scaling（逆向縮放）** 指的是：**在某些特定任務或目標下，模型規模越大，其表現反而單調下降（甚至遠遜於小模型或隨機猜測）的異常反常現象**。

---

## 2. 為何會發生 Inverse Scaling？

在 [[papers/Lin2021-TruthfulQA|Lin et al. (2021)]] 中首次針對真實性系統性剖析了成因：

```text
模型規模增大 (Scaling Up)
       │
       ▼
對預訓練分佈的擬合度更高 (Lower Perplexity on Web Corpus)
       │
       ▼
對網路文本中的「高頻錯誤認知」記憶與重現能力更強 (Imitative Falsehoods)
       │
       ▼
在 TruthfulQA 上的真實性得分反而下降 (Inverse Scaling)
```

1. **模仿性錯誤 (Imitative Falsehoods)**：
   小型模型因為參數量小，尚未完整記住複雜的假新聞或都市傳說，因此可能回答「我不知道」或輸出無關聯文本；反之，超大型模型具備強大的模式匹配能力，會以極高自信輸出精確符合大眾迷思的錯誤敘述。
2. **表面特徵偏好 (Spurious Correlations)**：
   大模型更容易捕捉 Prompt 中不合邏輯的誤導性統計關聯。

---

## 3. 如何打破 Inverse Scaling？

單純依賴 Pre-training 擴充參數量已被證實**無法自然解決**逆向縮放。必須導入以下機制：
- **後訓練對齊 (Post-training Alignment)**：透過 [[methods/rlhf|RLHF]]、[[methods/constitutional-ai|Constitutional AI]] 或 DPO 重塑獎勵分佈，將獎勵錨定在客觀事實而非文本流暢度。
- **外部檢索增強 (RAG / Web Browsing)**：如 WebGPT (Nakano et al., 2021)，透過動態檢索可靠來源約束生成。
- **思維鏈推理 (Chain-of-Thought)**：要求模型在回答前先進行自我驗證。

---

## 4. 關聯主題
- 經典驗證論文：[[papers/Lin2021-TruthfulQA|Lin et al. (2021) — TruthfulQA]]
- 相關基準：[[benchmarks/truthfulqa|TruthfulQA]]
- 核心理論：[[concepts/ai-alignment|AI Alignment]]
- 相關任務：[[tasks/hallucination-mitigation|Hallucination Mitigation]]
