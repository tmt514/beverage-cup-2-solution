# C - Heap Like Sort

## 題目大意

小 Heap 拿到一塊方形板子，對角線(右上 $$\leftrightarrow$$ 左下) 上面有一些相異的數字。我們對於每一個小格給予定義：

* **Open Cell**: 這格是空的而且這格的左、上、左上方向的所有格子都是空的。
* **Closed Cell**:
這格是空的而且這格的右、下、右下方向的所有格子都是空的。
* **Inner Cell**:
所有其他的格子。
* **Open-Only Cell**: 這格是 Open cell 但是非 Closed cell。

小 Heap 開始對這個方形板子上的數字進行操作：

1. 如果現在有任何 Inner cell，我們查看它緊鄰右邊或下面的格子，如果有任何數字的話，挑選較小的那個，把它拉進來。
2. 如果現在存在 