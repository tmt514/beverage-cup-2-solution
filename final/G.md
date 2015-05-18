# G - Strange Permutations

## 題目大意

排列 $$1$$ 到 $$n$$ 的整數，使得相鄰兩數互質，部分位置一定要填入某些數字，請問剩餘數字的填法方案數為何？

> <small>感謝 morris 提供題目大意！</small>

## 題解

其實我們可以把所有整數當做點、兩個整數是否互質作為建立邊的條件。所得到的圖之中，一個合法的排列便對應了圖上的一條 Hamiltonian Path。

### 動態規劃

一個簡單的想法即是：考慮「$$i=$$ 當前序列長度」、「$$S=$$ 哪些數字做過了」、「$$last =$$ 當前最末一個數是多少」，於是我們便有以下的遞迴轉移關係：

{% math %} dp[i][S][last] = \left\{
\begin{array}{ll}
0 & \mbox{若第 i 個位置不能是 last。}\\
\sum_{j\in S} dp[i-1][S \setminus \{last\}][j] & \mbox{其他}
\end{array}
\right.{% endmath %}

一個簡單的估計是：第一個維度 $$n$$，第二個維度 $$2^n$$，第三個維度 $$n$$；轉移是 $$O(n)$$，因此時間複雜度是 $$O(n^32^n)$$。但是真的是這樣嗎？

### 更仔細的分析

如同 Hamiltonian Path，我們也可以