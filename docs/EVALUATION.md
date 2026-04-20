# 評估標準

本專案不以單純最高報酬為唯一目標，綜合考量以下指標：

## 核心指標
- 總報酬
- 年化報酬
- 最大回撤
- Sharpe / Sortino
- 勝率
- 平均持有天數
- 交易次數
- 資金使用率

## 穩定性要求
- 不能只靠少數股票貢獻績效
- 不能只在單一月份或單一行情有效
- 必須比較不同股票、不同區段的表現
- 必須標示是否通過 walk-forward 或 out-of-sample 檢驗

## 評分方向
- 優先保留風險調整後績效較佳者
- 若報酬接近，優先保留回撤較低、規則較簡潔者
- 若策略過度複雜但提升有限，視為不優

## 參考總分公式
```text
score = return_score
      - drawdown_penalty
      - instability_penalty
      - overtrade_penalty
      - complexity_penalty
```

## 注意
實際總分公式可以再依你的風格調整，但不得只以最高報酬單一指標做保留依據。
