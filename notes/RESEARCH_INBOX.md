# RESEARCH_INBOX

這裡是人類與 OC / Agent 的研究任務入口。

使用方式：
- 人類把想法、問題、想測的方向先寫在這裡
- OC 讀到後，轉成 hypothesis 與 experiment
- 已處理項目不要刪，可改成狀態更新

---

## 狀態說明
- `NEW`：剛提出，尚未整理
- `TRIAGED`：已轉成研究題目
- `TESTING`：正在回測 / 分析
- `REVISE`：需要下一輪修正
- `DONE`：完成一輪研究
- `ARCHIVED`：已封存

---

## Inbox Items

### IDEA-001 | NEW
**Title:** 建立 AI 自我迭代策略研究流程

**Source:** Human

**Goal:**
讓人類提出想法後，OC / Agent 可以把 idea 轉成可回測假設，執行 baseline vs candidate 比較，留下失敗原因，並形成下一輪改進建議。

**Notes:**
- 研究系統不是自動下單系統
- 重點是可追蹤、可驗證、可重跑
- Git 要成為長期記憶與協作介面

**Next Step for OC:**
- 建立第一份 hypothesis card
- 建立第一份 experiment template
- 決定 baseline spec 的最小欄位

---

### IDEA-002 | NEW
**Title:** 評估 TimesFM 作為輔助模組而非主策略引擎

**Source:** Human

**Goal:**
評估 TimesFM 是否適合作為：
- forecast feature source
- volatility / uncertainty input
- regime filter 輔助

**Notes:**
- 不直接把 forecast 視為買賣訊號本體
- 先從輔助 filter / sizing 開始

**Next Step for OC:**
- 定義 TimesFM integration assumptions
- 列出最小測試方案
- 與 baseline 版本比較複雜度是否值得

---

### IDEA-003 | NEW
**Title:** 沿 baseline 主策略做資金配置最佳化

**Source:** Human

**Goal:**
研究當多檔股票同時出現訊號時，是否能透過排序、集中度限制、產業曝險限制與現金保留比例，提升組合效率並降低回撤。

**Next Step for OC:**
- 定義 allocation experiment scope
- 定義 portfolio-level metrics
- 建立第一份 allocation hypothesis
