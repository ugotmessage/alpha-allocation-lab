# Alpha Allocation Lab

這個專案用來研究一套既有主策略在「已篩選的優質股票池」上的最佳化版本。

重點不是重新發明交易法，而是沿著既有方法做：

1. 進出場條件微調
2. 停損 / 停利 / 加減碼優化
3. 多檔股票同時出現訊號時的資金配置
4. 在有限資本下提升整體組合效率
5. 降低最大回撤並提升穩定度

## 專案定位（新版）

本專案已擴充成一個 **AI 可持續迭代的策略研究工作區**。

定位如下：
- Human 提想法
- OC / Agent 將想法轉成 hypothesis
- 建立 candidate strategy spec
- 執行 baseline vs candidate 回測
- 紀錄失敗原因與 lessons
- 持續迭代，而不是只看單次最佳績效

**注意：本專案不是自動下單系統。**

## 專案原則

- 不追求單一年度最高報酬
- 優先追求可重複、可驗證、可解釋
- 所有改動都必須經過回測驗證
- 不得使用未來資料
- 不得為了回測績效過度扭曲原始主策略
- 若使用 XS Code，視為主策略原型，不直接假設平台執行結果可完全等價外部回測

## 建議工作流程

1. 把你的 XQ / XS Code 放進 `inputs/baseline_strategy.xs`
2. 在 `docs/STRATEGY_BASE.md` 補上主策略邏輯與核心 edge
3. 在 `docs/DATA_SPEC.md` 補上可用資料欄位
4. 先做 baseline backtest
5. 再開始做參數微調、資金配置與實驗紀錄

## OC / Agent 啟動入口

OC 進入本 repo 後，建議依序閱讀：

1. `AGENT.md`
2. `docs/AI-ITERATION-PLAN.md`
3. `docs/OC-GIT-COLLAB.md`
4. `docs/STRATEGY_BASE.md`
5. `notes/RESEARCH_INBOX.md`
6. `notes/LESSONS.md`

## 新增的研究協作檔案

### 計畫與規範
- `docs/AI-ITERATION-PLAN.md`：AI 自我迭代研究總計畫
- `docs/OC-GIT-COLLAB.md`：OC / Agent 透過 Git 協作的規範

### 研究記憶與協作入口
- `notes/RESEARCH_INBOX.md`：人類把想法丟進來的入口
- `notes/LESSONS.md`：研究過程中的長期經驗
- `hypotheses/`：每一個研究假設
- `experiments/`：每一輪實驗與比較結果

## 專案結構

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

## 第一版目標

第一版先專注在：

- 主策略拆解
- 可調參數定義
- 評分標準定義
- 實驗紀錄格式
- XS Code 匯入入口
- Human → OC → Git 的研究協作閉環

等你把主策略內容補上後，再往下做：

- baseline 對照組
- 參數掃描
- 多標的資金配置
- walk-forward 驗證
- 外部預測模組（例如 TimesFM）輔助整合

## 建議下一步

1. 補 `docs/STRATEGY_BASE.md`
2. 補 `docs/PARAMETER_SCOPE.md`
3. 補 `docs/DATA_SPEC.md`
4. 建第一份 hypothesis
5. 建第一份 baseline experiment
