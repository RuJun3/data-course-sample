# Collaborative filtering
## 目的
使用collaborative filtering推薦top-k商品給使用者。

## 方法
### 資料切分
訓練集：2018-09-01之前的ratings資料
測試集：2018-09-01\~2018-09-30之間的ratings資料

### 資料整理
* 將rating的unixReviewTime轉換成%Y-%M-%D的datetime形式

### 產生推薦
1. user-based collaborative filtering
	* 手刻user-based collaborative filtering
	* 不足k的推薦以rule-based(近一個月內評論最多的10個商品)來補齊推薦k個商品
2. item-based collaborative filtering
	* 手刻item-based collaborative filtering
	* 不足k的推薦以rule-based(近一個月內評論最多的10個商品)來補齊推薦k個商品
3. using surprise package
	* 若使用全部的training set會out of RAM，故使用近一年內的資料作為training set(2017-09-01\~2018-08-31)
	* algorithm：KNNBasic, similarity：cosine, min_support：2, user_based：False(item-based)
	* 不足k的推薦以rule-based(近一個月內評論最多的10個商品)來補齊推薦k個商品
## 結果
1. user-based collaborative filtering: 
	* 手刻user-based collaborative filtering： 0%
	* 不足k的推薦以rule-based來補齊推薦k個商品： 15.76%
2. item-based collaborative filtering
	* 手刻user-based collaborative filtering： 0.169%
	* 不足k的推薦以rule-based來補齊推薦k個商品： 15.59%
3. using surprise package
	* item-based: 0.339%
	* 不足k的推薦以rule-based來補齊推薦k個商品： 15.93%
