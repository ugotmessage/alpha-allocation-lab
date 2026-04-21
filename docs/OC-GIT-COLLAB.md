# OC Git Collaboration Protocol

本檔定義：**OC / Agent 如何透過 Git 與本專案協作**。

目標是讓研究流程不依賴單一 session 記憶，而是透過 repo 內的檔案持續接力。

---

## 核心原則

1. **Git 是共同記憶體**
   - 不把重要研究結論只留在聊天裡
   - 所有重要結論落到 repo 檔案

2. **一個 idea 對應一組可追蹤檔案**
   - hypothesis
   - strategy spec
   - experiment
   - decision

3. **先寫再做，做完再寫**
   - 開始前寫 hypothesis / task note
   - 做完後補 experiment / lessons

4. **不要覆蓋歷史**
   - 新一輪研究要新增紀錄，不是直接洗掉舊結論
   - allow revision，但保留脈絡

---

## 建議交流入口

### 人類 → OC
優先透過下列檔案讓 OC 理解任務：

- `notes/RESEARCH_INBOX.md`：新想法、待研究項目
- `docs/STRATEGY_BASE.md`：主策略核心精神
- `docs/PARAMETER_SCOPE.md`：允許調整的範圍
- `docs/DATA_SPEC.md`：可用資料來源

### OC → 人類
OC 每完成一輪研究，應更新：

- `experiments/YYYY-MM-DD-xxx.md`
- `notes/LESSONS.md`
- `docs/RESEARCH_LOG.md`

---

## 標準工作流

### 1. 收到新 idea
OC 應先：
- 讀 `AGENT.md`
- 讀 `docs/AI-ITERATION-PLAN.md`
- 讀 `docs/STRATEGY_BASE.md`
- 讀 `notes/RESEARCH_INBOX.md`
- 檢查是否已有重複 hypothesis / experiment

### 2. 建立 hypothesis
新檔命名建議：
- `hypotheses/hyp_YYYYMMDD_slug.md`

建議內容：
- title
- thesis
- expected edge
- risks
- regime
- next action

### 3. 建立實驗紀錄
新檔命名建議：
- `experiments/exp_YYYYMMDD_slug.md`

建議內容：
- baseline version
- candidate version
- changed variables
- test range
- evaluation summary
- failure analysis
- decision

### 4. 完成後更新總表
至少更新：
- `docs/RESEARCH_LOG.md`
- `notes/LESSONS.md`

---

## Commit 規則

建議使用以下 prefix：

- `docs:` 文檔更新
- `research:` 新 hypothesis / 新實驗
- `backtest:` 回測結果
- `lesson:` 經驗整理
- `promote:` 候選升級
- `archive:` 封存舊研究

### 範例
- `research: add volatility contraction hypothesis`
- `backtest: compare baseline vs candidate breakout filter`
- `lesson: record overfitting risk in short sample`

---

## OC 每輪輸出最低要求

每次研究結束，OC 不可只說「這版比較好」。

至少要留下：

1. **假設是什麼**
2. **改了哪些規則**
3. **測了哪些區間 / 標的**
4. **結果如何**
5. **風險在哪裡**
6. **是否值得下一輪**

---

## 與 TimesFM 協作的規則

若未來引入 forecasting module：

1. TimesFM 只作為輔助訊號來源
2. 不可直接把 forecast 當保證
3. 實驗紀錄中要明確標註：
   - forecast horizon
   - feature usage
   - 是否增加穩定性
   - 是否只是增加複雜度卻沒改善

---

## 禁止事項

- 不可只保留成功案例
- 不可跳過 baseline 對照
- 不可只根據單一年份結論 promote
- 不可把聊天中的推論當成已驗證事實
- 不可未經紀錄就大幅修改主策略精神

---

## 建議未來擴充

未來可以讓 OC 進一步支援：

- 自動掃描 `notes/RESEARCH_INBOX.md` 新任務
- 自動生成 hypothesis 草稿
- 自動填實驗模板
- 自動整理 lessons 到總表
- 自動比較近期候選版本並生成週報
