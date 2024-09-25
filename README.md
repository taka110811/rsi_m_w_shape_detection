# シグナル名: `rsi_m_w_shape_detection`

---

## このシグナルのスコープ
このシグナルが適用される範囲や条件を示します。

- **スコープ1**: RSIのダブルトップ（M字）の検出
- **スコープ2**: RSIのダブルボトム（W字）の検出

---

## より精度を高めるためのフィルタリング機能
このシグナルの精度を高めるために適用されるフィルタリング機能を列挙し、説明します。

- **機能1**: M字ではRSIが60以下ではシグナルなし
- **機能2**: W字ではRSIが40以上ではシグナルなし

---

## シグナルのロジック
このシグナルがどのように機能するか、具体的なロジックを説明します。シグナルがどのように計算され、どの条件下でトリガーされるかを記述します。

- **説明**: 〇〇の指標を元に、△△の基準で異常検知を行うロジック。例えば、RSIが70を超えた場合にアラートを発生させる等。

```mermaid
graph TD
    A[RSIの計算] --> B{RSIの変化量が条件を満たすか}
    B -->|M字型| M1[最初の上昇: 10〜20ポイント] --> M2[小さな下降: -6〜-1ポイント] --> M3[2回目の上昇: 2〜7ポイント] --> M_Detected[M字型検知]
    B -->|W字型| W1[最初の下降: -10〜-20ポイント] --> W2[小さな上昇: 1〜6ポイント] --> W3[2回目の下降: -2〜-7ポイント] --> W_Detected[W字型検知]
    
    M_Detected --> M_Signal{RSIが60以上か} -->|Yes| MS[シグナル生成: M字型]
    W_Detected --> W_Signal{RSIが40以下か} -->|Yes| WS[シグナル生成: W字型]

    MS --> Reset[状態のリセット]
    WS --> Reset

    Reset -->|M字型リセット| R1[最初の上昇検出をリセット]
    Reset -->|W字型リセット| R2[最初の下降検出をリセット]
    
    R1 --> R3[小さな変動検出をリセット] --> R4[M字型フラグをリセット]
    R2 --> R5[小さな変動検出をリセット] --> R6[W字型フラグをリセット]
```
