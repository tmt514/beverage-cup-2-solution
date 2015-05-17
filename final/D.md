# D - A Parking Problem

## 題目大意

停車場有 $$n$$ 個位置呈現單方向，由入口到出口分別編號為 $$1$$ 到 $$n$$，現在有 $$m$$ 名駕駛準備要停車，每名駕駛的停車方案都會先開到偏愛的車位上，如果發現已經有人停過，則會往後找一個空車位。由於駕駛入停車場任意順序。請問從 $$m$$ 個駕駛中挑出 $$n$$ 個駕駛，任意進入停車場，按照他們各自偏愛的停車方法，每一位都有停車位的合法選擇駕駛的方案數。

> <small>感謝 morris 協助提供題目大意，與題解說明！</small>

## 題解

維護前 $$i$$ 個位置中，挑選 $$j$$ 名駕駛的方法數！ $$dp[i][j]$$ 表示前 $$i$$ 個位置，挑選 $$j$$ 個駕駛的方法數，並且滿足 $$j\ge  i$$，否則會有留空一格造成後續的非法解。窮舉下一個位置挑選的人數 $$k$$，得到

$$dp[i+1][j+k] += (dp[i][j] * C[A[i+1]][k])\%MOD$$

由於兩個維度分別只要枚舉 $$0$$ 到 $$n$$ 就好，因此這樣計算的時間複雜度是 $$O(n^3)$$。

## 不算故事的故事

這部份跟解題無關。只是想跟大家分享一下 Parking function 的故事和一些性質。可以參考 [MIT 的投影片](http://www-math.mit.edu/~rstan/transparencies/parking3.pdf)。

什麼是 Parking function 呢？基本上就是一個長度為 $$n$$ 的序列 $$\alpha$$，它的每一項都是 $$1$$ 到 $$n$$ （基本上就是每個人的偏好停車位），若所有人「依照這個順序」進入停車場，都可以順利的把車子停進去，那麼我們稱這個序列 $$\alpha$$ 為一個 parking function。

對於一個固定的 $$n$$，究竟有多少 parking functions 呢？很令人意外地，答案出奇地簡單：我們令 $$f(n)$$ 表示長度為 $$n$$ 的 parking functions 數量。那麼恰恰好有

$$f(n) = (n+1)^{n-1}$$

這麼多種方法！

在 1959 年，Ronald Pyke 發現並證明了這個定理、Alan Konheim 和 Benjamin Weiss 在 1966 年也獨立做出了這個結果。但是直到 1974 年由 Pollak 給出了一個超輕巧與精采的組合證明。

大家還有在什麼地方看過這樣的公式？沒錯！就是 [Cayley's Formula 標號樹的計數](http://en.wikipedia.org/wiki/Cayley%27s_formula)！那麼必定有其對應關係吧！這個對應有兩種，一種是透過 [Prüfer 序列](http://en.wikipedia.org/wiki/Pr%C3%BCfer_sequence) 對一棵標號樹進行編碼。另一個則是透過 BFS 走訪記錄每個節點被發現的時間，直接對應到一個 parking function。大家有興趣也可以想看看，網路上也有相當多的資料可以參考～

除此之外，還可以參考賴俊儒學長以前的[科展內容](http://www.sec.ntnu.edu.tw/cultivation/92%E5%B9%B4/%E6%95%B8/%E8%B3%B4%E4%BF%8A%E5%84%92.pdf)，主要在描述 parking function 與另一個有趣遊戲 Chip-firing game 之間的關係。不過文章內也有提到一些關於 parking function 之中的有趣性質！