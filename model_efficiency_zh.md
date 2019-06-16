# 各模型計算效率分析

## 計算效率
計算量提高一倍，約可增加棋力一段。故一個較大的模型如果在同樣 Playouts 之下棋力強了 N 段，但每秒 Playouts 數卻小於 2^N 分之一，則在相同計算量（或行棋時間）限制之下（尤其在「非 GPU 環境」），棋力反而較弱。
所以我們可以定義計算效率:
取一個模型為基準，定為 1.0，其他模型的計算效率定為 (每秒相對 Playouts) 除以 (2 的 (段級差) 次方)

## 結論
- **LZ 157** 與 **ELF v2** 計算效率最高; 在相同計算時間之下，應具有近似的棋力
- 然而由於 **LZ 157** 的模型更小，更適合在小設備上運行
- 並且由於 LZ 157 的每秒 Playouts 數是 ELF v2 的兩倍，在大手數大龍攻殺時更有優勢


| SN | Name | Structure | 棋力 |  每秒相對 Playouts | 計算效率 |
| --- | --- | --------- | --- | ------------- | --- | 
|1 | LZ 226 | 40x256 | 15D | 0.1 | 0.4|
|2 | ELF v2 | 20x224 | 14D |  0.5 | 1.0 |
|3| **LZ 157**| 15x192 | 13D | 1.0 |**1.0**|
|4 | LZ 116 | 10x128 | 9D | 3.6 | 0.22|
|5 | LZ 091 | 6x128 | 6D | 5.9 | 0.05|
|6 | LZ ZQ F1 | 5x64 | 5D | 10.0 | 0.04|
|7 | LZ 057 | 5x64 | 2D | 10.0 | 0.005|

- 每秒 Playouts 以 LZ 157 為基底
- 棋力指 Playouts 1600 時的棋力

## 參考文獻
- https://github.com/breakwa11/GoAIRatings