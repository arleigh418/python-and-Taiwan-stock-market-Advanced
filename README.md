# Python 金融市場賺大錢聖經：寫出你的專屬指標-進階技術補充
博客來: https://www.books.com.tw/products/0010901963?loc=M_0039_001

momo: https://m.momoshop.com.tw/goods.momo?i_code=9261467

天瓏: https://www.tenlong.com.tw/products/9789860776294

誠品: https://www.eslite.com/product/1001313432682066432001

<br>

## 快速索引

[LINE消息推送](https://github.com/arleigh418/python-and-Taiwan-stock-market-Advanced#%E7%9B%B8%E9%97%9C%E6%8A%80%E8%A1%93%E8%A3%9C%E5%85%85%E5%8D%801---%E6%B6%88%E6%81%AF%E6%8E%A8%E9%80%81)

[backtrader-以web方式呈現買賣成果](https://github.com/arleigh418/python-and-Taiwan-stock-market-Advanced#%E7%9B%B8%E9%97%9C%E6%8A%80%E8%A1%93%E8%A3%9C%E5%85%85%E5%8D%802---%E4%BB%A5web%E5%BD%A2%E5%BC%8F%E5%B1%95%E7%8F%BE%E7%B5%90%E6%9E%9C)

[yfinance獲得分K資料](https://github.com/arleigh418/python-and-Taiwan-stock-market-Advanced/blob/main/README.md#%E7%9B%B8%E9%97%9C%E6%8A%80%E8%A1%93%E8%A3%9C%E5%85%85%E5%8D%803---yfinance%E7%8D%B2%E5%8F%96%E6%AF%8F%E5%88%86%E9%90%98%E8%B3%87%E6%96%99)


<br>


## 相關技術補充區
### 相關技術補充區1 - 消息推送
關於消息推送我們是利用mail的形式，因為mail的應用比較廣，也比較正式，通常稍微大型的公司行號都比較不接受使用Line發送一些程式訊息。

但如果你想用Line發送，有個非常簡單的方式，那就是Line notify。

這篇文章寫得很清楚，推薦給大家 : https://ithelp.ithome.com.tw/articles/10234115

步驟很簡單:
1. 下載下這位大神提供的程式
2. 至Line申請token (文章有給申請網址)，然後你可以創建一個空群組，在申請Token的畫面中選擇該空群組
3. 把LINE Notify這位官方帳號邀請到你的空群組
4. 執行1.下載下來的程式即可成功推播


<br>


### 相關技術補充區2 - 以web形式展現結果
在使用backtrader回測時，我常常會收到使用者要求買賣切入點不要使用圖，他們希望能夠滑鼠移過去就能看到買賣時的價格。

其實是有辦法的，在書中沒有介紹主要是考量這個並不是官方支援的套件，也非一個團隊負責維護的，這類型的套件有可能過幾年作者因事務繁忙而缺乏維護失效，不過目前作者還是有在維護的，因此可以使用沒問題。

該篇專案: https://github.com/verybadsoldier/backtrader_plotting

步驟如下:
1. 安裝套件 pip install backtrader_plotting
2. import套件
```
from backtrader_plotting import Bokeh
from backtrader_plotting.schemes import Tradimo
```

3. 在cerebo.adddata中加入name，套件畫圖需要指定資料名稱
```
cerebro.adddata(data,name='2330.TW')
```

4. 引用Bokeh類，style=bar代表k棒圖；output_mode常用的有save(儲存)跟show(顯示)，如果是範例的儲存則要給予filename，也就是儲存位置；scheme則是樣式選擇。
```
b = Bokeh(style='bar', output_mode='save',filename=f'png/result_{stock}.html' ,scheme=Tradimo())
cerebro.plot(b)
```

完成後你就可以在指定的位置看到html檔案，用chrome打開來看就能達到我們要的效果，可以嘗試看看。


<br>


### 相關技術補充區3 - yfinance獲取每分鐘資料
yfinance利用interval參數支援獲得分K的資料，不過如果是最短的1分K目前只支援7天的期間。
除日K之外，其他時間架構大部分都有限區間(例如1分限7天的資料)，因此在書中沒有介紹，因為我自己覺得實用度其實不太高的，大抵上我都是使用其他的資料源如券商，不過還是分享給你。
```
data = yf.download(tickers = '2330.TW' ,start ='2021-08-18',end='2021-08-21', interval = '1m')
data
```

api所提供的時間架構:
```
[1m, 2m, 5m, 15m, 30m, 60m, 90m, 1h, 1d, 5d, 1wk, 1mo, 3mo]
```


<br>

