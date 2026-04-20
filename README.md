# Alpha Allocation Lab

這個專案用來研究一套既有主策略在「已篩選的優質股票池」上的最佳化版本。

重點不是重新發明交易法，而是沿著既有方法做：

1. 進出場條件微調
2. 停損 / 停利 / 加減碼優化
3. 多檔股票同時出現訊號時的資金配置
4. 在有限資本下提升整體組合效率
5. 降低最大回撤並提升穩定度

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

## 專案結構

```text
alpha-allocation-lab/
├─ README.md
├─ AGENT.md
├─ docs/
│  ├─ STRATEGY_BASE.md
│  ├─ PARAMETER_SCOPE.md
│  ├─ DATA_SPEC.md
│  ├─ EVALUATION.md
│  └─ RESEARCH_LOG.md
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

等你把主策略內容補上後，再往下做：

- baseline 對照組
- 參數掃描
- 多標的資金配置
- walk-forward 驗證
