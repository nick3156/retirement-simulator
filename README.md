# retirement-simulator (archived)

> **Moved**: このリタイア/FIRE シミュレータは [Kanjo](https://fixed-cost.tz3156.workers.dev/simulator) (お金まわり統合ハブ) に統合された。今後のメンテはそちらで行う。ここに残しているのは履歴用の単一HTML。

- Kanjo (移行先): https://fixed-cost.tz3156.workers.dev/simulator
- Kanjo のソース: https://github.com/nick3156/fixed-cost (private)
- 旧 公開URL: https://nick3156.github.io/retirement-simulator/ (GitHub Pages は当面残す)

## もともと

単一HTMLで動くリタイア/FIREシミュレータ。現在の資産・積立・想定利回り・インフレ率・年金条件から、リタイア後に資金が何歳まで持つかを可視化する。

## 特徴

- 月次複利でのシミュレーション（積立・取り崩しを月単位で計算）
- 年金のインフレ調整オプション（デフォルトON / OFFで保守シナリオ）
- 4%ルールに基づくFIRE達成ラインの自動算出
- 目標資産額からの必要積立額の逆算（FV-of-annuity）
- 入力値は localStorage に自動保存

Kanjo 側では計算ロジックは完全踏襲し、UI と localStorage キー (`retirement-sim-values-v2`) も互換を維持。旧ブラウザで入力した値は Kanjo 側でも復元される。

## ファイル

- `index.html` — シミュレータ本体（単一HTML）

## ローカルで動かす

ブラウザで直接開くだけで動作。ビルド不要。

```
open index.html
```

## 計算の前提

- 利回りは税引後の年率を想定。月次複利 `(1+r)^(1/12)-1` で回す
- 積立は月末拠出（end-of-period）
- 取り崩しは月初に生活費を引いて残りを1ヶ月運用
- 生活費は常にインフレ調整後の名目値
- 年金は詳細設定で実質固定(ON) / 名目固定(OFF) を切替
- 生活防衛資金（現金）は運用・取り崩しに含めずチャートの参照ラインとしてのみ表示
