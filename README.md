# アプリの概要
### フリーマーケットのアプリケーションを作成しました。
![画像の説明](https://i.gyazo.com/d9ef649dec804033338536dafd110b0a.png)

## 開発状況
#### 開発環境  
・Ruby/Ruby on Rails/MySQL/Github/AWS/Visual Studio Code  
#### 開発期間と平均作業時間  
・開発期間：約4週間  
・1日あたりの平均作業時間：約9時間  
#### 開発体制
・人数：5名  
・アジャイル型開発（スクラム）  
・Trelloによるタスク管理  

## 実装機能
![](https://i.gyazo.com/30609fd5419baa4a37efae0f69e47333.png)  
![](https://i.gyazo.com/144444657ffa4e784ec03e3fec7adfe1.png)

##  usersテーブル
|Column|Type|Options|
|------|----|-------|
|nickname|string|null: false|
|email|string|null: false, unique: true|
|password|string|null: false|
|last_name|string|null: false|
|first_name|string|null: false|
|last_name_kana|string|null: false|
|first_name_kana|string|null: false|
|birthday|date|null: false|
### Association
- has_many :seller_items, foreign_key: "seller_id", class_name: "items"
- has_many :buyer_items, foreign_key: "buyer_id", class_name: "items"
- has_many :bookmarks, dependent: :destroy
- has_many :bookmark_items, through: :bookmarks, source: :item
- has_one :sending_destination, dependent: :destroy
- has_one :credit_card, dependent: :destroy
- hsa_one :sns_authentication, dependent: destroy

##  addressesテーブル
|Column|Type|Options|
|------|----|-------|
|destination_last_name|string|null: false|
|destination_first_name|string|null: false|
|destination_last_name_kana|string|null: false|
|destination_first_name_kana|string|null: false|
|post_code|integer(7)|null: false|
|prefecture_id|integer|null: false|
|city|string|null: false|
|address|string|null: false|
|building_name|string||
|phone_number|bigint|unique: true|
|user|references|null: false|
### Association
- belongs_to :user
- belongs_to_active_hash :prefecture

##  credit_cardsテーブル
|Column|Type|Options|
|------|----|-------|
|customer_id|string|null: false|
|card_id|integer|null: false|
|user|references|null: false, foreign_key: true|
### Association
- belongs_to :user

##  itemsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|introduce|text|null: false|
|category_id|references|null: false|
|brand|references||
|condition_id|string|null: false|
|delivery|references|null: false, foreign_key: true|
|prefecture_id|integer|null: false|
|preparation_id|integer|null: false|
|buyer_id|integer||
|seller_id|integer|null: false|
|price|integer|null: false|
### Association
- has_many: images, dependent: :destroy
- has_many: bookmarks, dependent: :destroy
- belongs_to :category
- belongs_to :brand
- belongs_to_active_hash :condition
- belongs_to :delivery
- belongs_to_active_hash :preparation
- belongs_to :seller, class_name: "User"
- belongs_to :buyer, class_name: "User
- belongs_to_active_hash :prefecture

##  imagesテーブル
|Column|Type|Options|
|------|----|-------|
|item|references|null: false, foreign_key: true|
|url|string|null: false|
### Association
- belongs_to :item

##  categoriesテーブル
|Column|Type|Options|
|------|----|-------|
|name|string|null: false|
|ancestry|string|null: false|
### Association
- has_many: items

##  brandsテーブル
|Column|Type|Options|
|------|----|-------|
|name|string||
### Association
- has_many: items

##  conditionsテーブル
|Column|Type|Options|
|------|----|-------|
|condition|string|null: false|
### Association
- has_many: items

##  deliveriesテーブル
|Column|Type|Options|
|------|----|-------|
|method|string|null: false|
|ancestry|string|null: false|
### Association
- has_many: items

##  preparationsテーブル
|Column|Type|Options|
|------|----|-------|
|preparation|string|null: false|
### Association
- has_many: items

##  prefecturesテーブル
|Column|Type|Options|
|------|----|-------|
|prefecture|string|null: false|
### Association
- has_many: items
- has_many: addresses

##  bookmarksテーブル
|Column|Type|Options|
|------|----|-------|
|user|references|null: false, foreign_key: true|
|item|references|null: false, foreign_key: true|
### Association
- belongs_to: user
- belongs_to: item



* Database initialization

* How to run the test suite

* Services (job queues, cache servers, search engines, etc.)

* Deployment instructions

* ...
