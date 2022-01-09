實作「Collaborative filtering」的推薦系統

專案目的
建立一個推薦系統，推薦商品給曾經在Mimi Beauty網站上購買過美妝商品的客戶。

執行方式
透過分析美妝產品資料(product data)、用戶評分資料(review data)，設計推薦邏輯，推薦商品給客戶。

資料切割方式
Training data：
近三個月資料：DATE >= 2018-06-01, DATE < 2018-09-01
Testing data：
review data:：DATE >= 2018-09-01, DATE < 2018-09-30

資料清洗

rating 刪除完全重複資料
同個 user 對同個 item 的重複評分資料，只保留最新評論資料
篩選最低評論次數>= 3次的使用者
不足部分以作業1之rule-based推薦產品補足

推薦邏輯
1) User-based Collaborative Filtering
2) Item-based Collaborative Filtering
3) Collaborative Filtering by surprise package
4) 拉長測試、訓練集時間，觀察CF是否有成功推薦。
Train ：2017-07-01 - 2018-02-28
Test ：2018-02-28 - 2018-09-30

推薦結果
1st.：0.133 ( Rule Based ) / 0(User-based Collaborative Filtering) / 0.133(CF + Rule Based)
2nd.：0.133 ( Rule Based ) / 0(Item-based Collaborative Filtering) / 0.133(CF + Rule Based)
3rd.：0.133 ( Rule Based ) / 0(Collaborative Filtering by surprise package) / 0.133(CF + Rule Based)
4th.：0.1149 ( Rule Based ) / 0.0009(Collaborative Filtering by surprise package) / 0.11437(CF + Rule Based)

總結：

1.本週加入內容的推薦方式，Recall效果並沒有因此增加，原因與作業二一樣，測試集九月分中584人中僅有38人用戶有出現在訓練集中，而且也沒因為出現在訓練集中成功推薦給他，因此38人中對於內容推薦是都沒有命中測試集的購買清單。

2.本次則多增加切割測試/訓練資料，觀察測試資料中的使用者是否出現在訓練資料中，並挑選其中較多使用者重複出現的情況下再進行推薦。
發現在使用者重疊比較多的情況下，協同過濾確實是有推薦成功商品的，但準確率極低的情況下在觀察資料下發現可能原因為大多數的使用者(99%)的評論次數是小於3次的，所以在計算的時候已經先排除99%的使用者，因此樣本數過少的情況下反而推薦的商品也不一定準確。
