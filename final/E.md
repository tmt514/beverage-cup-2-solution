# E - Kirino in Google Code Jam

## 中文題目

桐乃最喜歡哥哥了！現在她的哥哥為了專心準備大學聯考而搬出去一個人住，桐乃為了慰勞哥哥所以每天幫哥哥做早餐！今天 (2015/4/8) 桐乃和哥哥約好早上十點要送早餐過去，可是一早醒來卻發現早上 9:00 ~ 11:30 是 Google Code Jam 的 Round 1A，好在這個 Round 的題目對桐乃來說並不太難，她在三十分鐘左右就完成了所有題目。但要上傳答案前卻發現有一些測試資料能讓她的程式碼 WA 掉，但桐乃一時間不知道該如何解決這個 Bug，桐乃心想：「啊啊啊算了啦，就放它去吧，哥哥比較重要！我就直接上傳並趕緊幫哥哥做早餐！」於是桐乃如期送早餐去給哥哥了。

送完早餐回到家後，比賽已經結束了，桐乃發現她所有上傳的答案都被評為正確！？這時她傻笑的說：「嘿嘿嘿～這一定是我對哥哥的愛所賜的祝福吧 :D」
![KirinoSmile](https://lh6.googleusercontent.com/rJCCrzXUNYCLyxKD8QXQDM8QjEhjEaLrYwB5-Q54NO4TFg9ShmnhzJZGa5T2SO-WDKr1PDZk=w1342-h561-rw)

從這個故事我們可以注意到，要生測資實屬不易，實際上能讓桐乃 WA 掉的測資，可以讓不少人的 code 都 WA 掉，若比賽的正式測資存在這樣的測資的話，比賽結將會大大的不同吧？

現在問題來了，你能夠生出讓桐乃該題 WA 掉的測資嗎？

[要看該題題目敘述請點這 ( Problem C Logging )](http://code.google.com/codejam/contest/4224486/dashboard#s=p2)

[要找到桐乃(Kirino)的程式碼請點這](http://code.google.com/codejam/contest/4224486/scoreboard?c=4224486#vt=1&vf=1)

## 簡化題意

請找到一組能讓 2015 年 Google Code Jam Round 1A 第三名第三題的Code WA 的測資。

## 題解

要生出讓該 code WA 掉的測資，首先，你要知道 Bug 在哪。但這份程式碼若只考慮它的邏輯正確性，大概是找不出任何 Bug 吧？若非邏輯錯誤，Bug 會是在哪呢？答案是浮點數的精確度不足。該份 code 的浮點數誤差(EPS)使用的數值為 $$10^{-12}$$，但實際上在本題的最小的夾角角度差比 $$10^{-12}$$ 還小，使用這個數值來判斷兩個代表角度的浮點數是否相等，