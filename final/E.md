# E - Kirino in Google Code Jam

## 中文題目

桐乃最喜歡哥哥了！現在她的哥哥為了專心準備大學聯考而搬出去一個人住，桐乃為了慰勞哥哥所以每天幫哥哥做早餐！今天 (2015/4/8) 桐乃和哥哥約好早上十點要送早餐過去，可是一早醒來卻發現早上 9:00 ~ 11:30 是 Google Code Jam 的 Round 1A，好在這個 Round 的題目對桐乃來說並不太難，她在三十分鐘左右就完成了所有題目。但要上傳答案前卻發現有一些測試資料能讓她的程式碼 WA 掉，但桐乃一時間不知道該如何解決這個 Bug，桐乃心想：「啊啊啊算了啦，就放它去吧，哥哥比較重要！我就直接上傳並趕緊幫哥哥做早餐！」於是桐乃如期送早餐去給哥哥了。

送完早餐回到家後，比賽已經結束了，桐乃發現她所有上傳的答案都被評為正確！？這時她傻笑的說：「嘿嘿嘿～這一定是我對哥哥的愛所賜的祝福吧 :D」

![](KirinoSmile.jpg)


從這個故事我們可以注意到，要生測資實屬不易，實際上能讓桐乃 WA 掉的測資，可以讓不少人的 code 都 WA 掉，若比賽的正式測資存在這樣的測資的話，比賽結將會大大的不同吧？

現在問題來了，你能夠生出讓桐乃該題 WA 掉的測資嗎？

[要看該題題目敘述請點這 ( Problem C Logging )](http://code.google.com/codejam/contest/4224486/dashboard#s=p2)

[要找到桐乃(Kirino)的程式碼請點這](http://code.google.com/codejam/contest/4224486/scoreboard?c=4224486#vt=1&vf=1)

## 簡化題意

請找到一組能讓 2015 年 Google Code Jam Round 1A 第三名第三題的 Code WA 的測資。

## 原題解答

在解這題之前請先了解原題的做法，可參考 [官方題解](http://code.google.com/codejam/contest/4224486/dashboard#s=a&a=2) 或 [jo4 的 Blog](http://jo4-code.blogspot.tw/2015/04/2015GCJ-Round1A.html) 或 [Morris 的 Blog](http://morris821028.github.io/2015/04/20/2015-google-code-jam-1A/)

P.S. 我出這題的靈感如下：某天我看到 jo4 的 Blog 題到我的 Code，我就感到非常慌張，因為我不確定我的 code 中 **EPS** 值是否恰當，深怕其他人看到我的 code 會誤以為只要為 $$10^{-12}$$ 就夠了，仔細研究一下就發現我 **EPS** 真的設太大了...

## 題解

要生出讓該 code WA 掉的測資，首先，你要知道 Bug 在哪。但這份程式碼若只考慮它的邏輯正確性，大概是找不出任何 Bug 吧？若非邏輯錯誤，Bug 會是在哪呢？答案是浮點數的精確度不足。該份 code 的浮點數誤差(EPS)使用的數值為 $$10^{-12}$$，但在本題的數據範圍下，這樣的數值並不夠小，有機會產生誤判。

以下為導致 WA 的程式碼區塊：
``` cpp
for(int j=0;j<vn*2;j++){ // 原code這個for迴圈是使用Macro
    while(v[ll]+PI+1e-12<v[j])ll++;
    if(j>=vn)ma=max(ma,j-ll+1);
}
```
在 while 迴圈裡想要判斷是否 `v[ll] + PI < v[j]`，因為浮點數的運算有機會產生非常小的誤差，使得運算的結果比真實數值還小，於是通常我們會額外加一個稍為比電腦的計算誤差大一點的數值 $$EPS$$ 來避免誤判，但 $$EPS$$ 若設太大，就會有機會使得原本不等式會成立卻變成不成立了。而我們要讓這份程式碼 WA 掉，至少要先找出什麼時候會不等式本該成立卻變成不成立。這這個問題可根據 `v[ll]` 和 `v[j]` 產生的方法追本溯源變為**尋找平面上夾角介於 $$\pi- 10^{-12}$$ 和 $$\pi$$ 之間的三個整數座標點**。

現在把此問題轉為數學式：請找出兩個整數座標的向量 $$\vec{v1}$$ 和 $$\vec{v2}$$ ，使得這兩個向量夾角 $$\theta$$ 滿足 $$\pi - 10^{-12} < \theta < \pi $$。

很接近 $$\pi$$ 的夾角對大家來說可能比較難想像，那我們把向量 $$\vec{v1}$$ 反向，於是所求也可想像成 $$- \vec{v1}$$ 和 $$\vec{v2}$$  的夾角必須小於 $$10^{-12}$$。

現在我們就來想想，平面上給定座標範圍最接近的兩個夾角可以多小？這個問題[在 Codefoces 的 Blog 上有某人給了解答](http://codeforces.com/blog/entry/17602)。但我用我自己的方法來解釋，因為兩向量夾角 $$\theta$$ 很小時，擁有公式 $$\theta \approx \sin{\theta} = \frac{\vec{v1} \times \vec{v2}}{|\vec{v1}|*|\vec{v2}|}$$，其中分子 $$\vec{v1} \times \vec{v2}$$ 由於座標都是整數又非零，所以最小的可能值為 $$1$$，而分母最大的可能情形為在限制範圍內最遠的兩個點座標距離平方，也就是 $$8*10^{12}$$，於是我們就能估出任兩個不同方向的最小夾角至少為 $$\frac{1}{8*10^{12}} \approx 1.25*10^{-13}$$。哇！！！原來有辦法估出那麼精準的下界！有沒有很驚訝呢？(小月自己發現這件事時是非常驚訝啦！因為類似題目見了超多次，我都是隨便使用一個 **EPS**  值，從沒好好估過，經過這次經驗以後就知道要怎麼估了。)

但只是估出下界還不足以解出這題，現在我們不是要解出原題，而是要構造一組極限的測試資料。這時我們就要利用一個簡單的恆等式：$$x^2 - (x+1)*(x-1) = 1$$ 而構造出三個座標點 $$(0,0), (1999999,1999998), (2000000,1999999)$$用電腦算一下這三個點最小的夾角是 $$1.24971 * 10^{-13}$$，和我們估出來的下界非常接近吧！但實際上，我們要找的是接近 $$\pi$$ 的角度而不是接近 $$0$$ 的角度，這樣的話用類似方法構造出來的三個點應該會是 $$(0,0), (-999999,-999998), (1000000,999999)$$其夾角和 $$\pi$$ 的差距約為 $$5*10^{-13}$$，仍舊比 Kirino 所設的 EPS 還小。

找出很接近 $$\pi$$ 的角後我們還差一步，雖然我們已經讓 **while** 迴圈判斷錯誤，但若只有三個頂點， Kirino 的 Code 無論如何都還是能跑出正確答案，你至少要再加一個頂點才能讓此 Bug 產生對答案的副作用，而這最後這一步就留給大家自由發揮吧～

順帶一題，小月在測試的時候是生了一個 $$n = 4$$ 的答案，而至今為止 AC 的四個人有三個人八成也是用類似方法構造出了 $$n = 5$$ 的答案，而還有另一個參賽者採取完全不同的策略解這題：隨機生出大量的點來尋找夾角超小的頂點們，在想辦法用他們找到一組能使 Kirino WA 掉的測試資料，詳情請參考[該參賽者(Morris)的 Blog](http://morris821028.github.io/2015/05/15/tmt514-Beverage-Cup-2-E/)。