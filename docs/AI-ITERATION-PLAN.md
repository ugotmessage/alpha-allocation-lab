# AI Strategy Iteration Plan

## 目標

把本專案從「手動研究主策略最佳化」升級成「人類提出想法，AI/OC 負責拆解、測試、比較、記錄、迭代」的研究系統。

本專案**不是自動下單系統**。

本專案的定位是：

1. 接收研究想法
2. 轉成可驗證假設
3. 生成候選策略版本
4. 執行回測與比較
5. 分析失敗原因
6. 形成下一輪改進提案
7. 把結果以 Git 形式持久化，供 OC / Agent / 人類持續協作

---

## 角色分工

### Human（你）
- 提出研究方向與主觀想法
- 決定主策略核心精神不可被扭曲的邊界
- 最終批准哪些版本值得保留或升級

### OC / Agent
- 讀取 `AGENT.md`、本計畫、資料規格與研究紀錄
- 將人類的想法轉成 hypothesis
- 產出 candidate strategy spec
- 執行回測、比較、彙整失敗原因
- 將結果提交到 Git 檔案中

### 程式 / 回測引擎
- 做資料處理
- 執行可重跑回測
- 產出一致指標
- 防止 look-ahead / data leakage / 未計成本等錯誤

---

## 研究主軸

### 主軸 A：沿著 baseline 主策略做結構化優化
優先做：
- 停損 / 停利優化
- 進場 / 出場條件微調
- 初始倉位與加碼節奏
- 多檔訊號同時出現時的排序與資金配置
- 產業曝險與集中度控制

### 主軸 B：把外部預測模組當作輔助，而不是交易真相
例如 TimesFM 只應作為：
- filter
- risk sizing input
- regime 輔助判斷
- volatility / uncertainty feature source

不要直接把 forecast 值視為買賣訊號本體。

### 主軸 C：建立失敗知識庫
每次研究除了紀錄成功案例，也必須紀錄：
- 為何失敗
- 哪些市場階段失效
- 是否只是單一期間 overfit
- 交易成本是否吃掉 edge
- 是否因條件太多導致樣本過少

---

## 核心研究流程

### Step 1. 收 idea
來源：
- Human 口頭想法
- `notes/RESEARCH_INBOX.md`
- 舊研究紀錄
- 外部靈感（只能當靈感，不能直接採信）

### Step 2. 轉 hypothesis
每個 idea 要轉成標準假設，至少包含：
- `id`
- `title`
- `thesis`
- `expected_edge`
- `market`
- `timeframe`
- `risks`
- `expected_regime`

### Step 3. 編譯成 strategy spec
每個候選版本必須明確寫出：
- entry rules
- exit rules
- stop / take-profit
- sizing
- filters
- holding period
- cost assumptions

### Step 4. 跑 baseline vs candidate
每次至少比較：
- baseline
- candidate_A
- candidate_B（若有）
- optional forecast-assisted variant

### Step 5. 產出評估
每次回測必須輸出：
- total return
- CAGR
- max drawdown
- Sharpe
- Sortino
- profit factor
- win rate
- trade count
- turnover
- average hold days
- out-of-sample 表現
- walk-forward consistency

### Step 6. 寫失敗分析
每次都要回答：
- 這次改善是真的還是只是假優化？
- 主要 improvement 來自什麼？
- 風險是否變高？
- 哪個市場 regime 最脆弱？
- 下一輪應該改 entry / exit / sizing / filter 哪一類？

### Step 7. 寫入 Git
所有結論都要落檔，至少包含：
- hypothesis card
- strategy spec
- experiment result
- lesson learned
- promote / reject decision

---

## Promotion Gate

candidate 不得因為單一指標好看就升級。

### 必要條件
- 扣成本後仍有正向 edge
- 交易筆數足夠，不是極少數交易撐績效
- OOS 沒有明顯崩壞
- 最大回撤在可接受範圍
- 與 baseline 相比至少有一項重要提升
- 規則仍可解釋，沒有過度複雜化

### 一票否決
- look-ahead bias
- survivorship bias
- data leakage
- 未計成本
- 只在極短期間有效
- 參數極端敏感，鄰近值失效

---

## 建議檔案結構

```text
alpha-allocation-lab/
├─ README.md
├─ AGENT.md
├─ docs/
│  ├─ AI-ITERATION-PLAN.md
│  ├─ OC-GIT-COLLAB.md
│  ├─ STRATEGY_BASE.md
│  ├─ PARAMETER_SCOPE.md
│  ├─ DATA_SPEC.md
│  ├─ EVALUATION.md
│  └─ RESEARCH_LOG.md
├─ notes/
│  ├─ RESEARCH_INBOX.md
│  └─ LESSONS.md
├─ hypotheses/
│  └─ README.md
├─ experiments/
│  └─ README.md
├─ inputs/
│  ├─ baseline_strategy.xs
│  └─ README.md
├─ backtests/
│  └─ README.md
├─ src/
│  └─ README.md
└─ outputs/
   └─ README.md
```

---

## 第一階段（V1）

只做最小可行閉環：

1. Human 提一個 idea
2. OC 寫一份 hypothesis card
3. OC 建一個 candidate strategy spec
4. 跑 baseline 與 candidate 回測
5. 寫 experiment report
6. 決定保留 / 修正 / 淘汰

### V1 成功標準
- 同一個 idea 可以被完整追蹤
- 結果可重跑
- 失敗原因有落檔
- Git 歷史可看出研究演進

---

## 第二階段（V2）

- 引入多輪 mutation
- 建立 lesson cards
- 自動比較多個 candidate
- 開始接外部預測模組（例如 TimesFM）當輔助特徵

---

## 第三階段（V3）

- heartbeat / cron 定期研究
- 自動整理 research summary
- 自動推薦下一輪研究方向
- 更細的 portfolio allocation engine

---

## 實作原則

1. 先可追蹤，再求自動化
2. 先有 baseline，再做變異
3. 先保證資料正確，再談模型高級化
4. 先建立失敗知識，再追求高分數
5. 所有研究輸出都要能被未來的 OC 接續理解
