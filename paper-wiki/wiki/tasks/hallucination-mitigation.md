---
type: task
name: Hallucination Mitigation
aliases: [幻覺抑制, 幻覺緩解, Factuality Enhancement, 真實性增強]
tags: [task, hallucination, factuality, truthfulness]
---

# Hallucination Mitigation (幻覺抑制與真實性增強)

## 1. 任務定義與範疇
在大型語言模型中，**Hallucination（幻覺）** 指模型生成看似流暢、自信但實際上背離客觀事實、邏輯矛盾或與上下文依據不符的內容。

主要分為兩種型態：
1. **內部知識幻覺 (Factuality Hallucination)**：模型在開放式問答中捏造歷史事實、科學數據或引用不存在的文獻（例如 [[papers/Lin2021-TruthfulQA|TruthfulQA]] 所測量的問題）。
2. **忠實度幻覺 (Faithfulness Hallucination)**：在摘要、翻譯或 RAG 任務中，模型生成了給定參考上下文（Context）中未包含或相互矛盾的陳述。

---

## 2. 主流緩解技術範式
- **事實驗證對齊 (Factuality-aware Alignment)**：在 RLHF 或 DPO 過程中針對事實錯誤施加強烈懲罰。
- **檢索增強生成 (Retrieval-Augmented Generation, RAG)**：透過外掛搜尋引擎或私有知識庫，將知識檢索從參數記憶解耦。
- **自我糾錯與批判 (Self-Correction & Critique)**：借鑒 [[methods/constitutional-ai|Constitutional AI]] 的思想，要求模型在輸出後自我檢查真實性（如 Self-Refine、Factool）。

---

## 3. 關聯主題
- 核心評測基準：[[benchmarks/truthfulqa|TruthfulQA]]
- 理論瓶頸：[[concepts/inverse-scaling|Inverse Scaling]]
- 對齊整體目標：[[concepts/ai-alignment|AI Alignment (Honest Pillar)]]
