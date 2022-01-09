# Content-based filtering
## 目的
使用content-based filtering推薦top-k商品給使用者。
## 方法
### 資料切分
訓練集：2018-09-01之前的ratings資料
測試集：2018-09-01~2018-09-30之間的ratings資料
### 資料整理
* 根據ratings的時間在metadata加上last_review_date
* EDA後決定只留下asin, brand, title, price, description, last_review_date
* 整理各欄位：
	* 將是空list或空字串的轉換為nan
	* 整理price欄位：去掉$，將不是數字的部分轉為為nan
	* 整理description：將list內的元素合在一起成字串，nan的部分以title補上
	* 整理title, description：去除符號
* 根據rule-based的結果決定只使用近一個月內有評論的商品，以及testing users購買過的商品
### 產生推薦
* 舊戶：使用近一個月內有評論的商品，以及testing users購買過的商品產生計算tfidf，在使用cosine_similarity找出分數較高的top 10商品
* 新戶：推薦ratings訓練集中近一個月內評論最多的10個商品
## 結果
content-based filtering recall: 15.76%
較rule-based filtering recall提升4.6%
