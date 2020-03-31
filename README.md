# Title

### フリマ

# Overview


# Production environment

フリマ  
URL : http://18.180.99.238/    

テスト用アカウント等  
- 購入者用  
メールアドレス: gonza@gmail.com  
パスワード: 22222222  
- 購入用カード情報  
番号：4242424242424242  
期限：2024/02  
セキュリティコード：123  
- 出品者用  
メールアドレス名: doda@gmail.com  
パスワード: 11111111  
 
# Production background
 

# Ingenuity

# Environment & Technology used
 
* ruby 2.5.1  
* Rails 5.2.4.1  
  

# DEMO

- 出品者用テストアカウントでログイン→トップページから出品ボタン押下→商品情報入力→商品出品
- 購入者用テストアカウントでログイン→トップページのピックアップカテゴリーから
- 商品選択→商品購入
- 確認後、ログアウト処理をお願いします。

# To be implemented
 
- 検索機能
- お気に入り機能
- パンくず導入
- コメント機能

# DB

## usersテーブル
|Column|Type|Options|
|------|----|-------|
| nickname           | string | null: false |
| email              | string | null: false |
| encrypted_password | string | null: false |
| user_image         | string ||
| introduction       | text   ||
| family_name        | string | null: false |
| first_name         | string | null: false |
| family_name_kana   | string | null: false |
| first_name_kana    | string | null: false |
| birth_day          | date   | null: false |

### Association
- has_many   :products       dependent: :destroy
- belongs_to :destination    dependent: :destroy
- belongs_to :card           dependent: :destroy


## destinationテーブル
|Column|Type|Options|
|------|----|-------|
| user_id          | integer | null: false, foreign_key: true|
| family_name      | string  | null: false|
| first_name       | string  | null: false|
| family_name_kana | string  | null: false|
| first_name_kane  | string  | null: false|
| post_code        | string  | null: false|
| prefecture       | string  | null: false|
| city             | string  | null: false|
| address          | string  | null: false|
| building_name    | string  ||
| phone_number     | string  ||

### Association
- belongs_to :user


## cardテーブル
|Column|Type|Options|
|------|----|-------|
| user_id     | integer | null: false, foreign_key: true |
| customer_id | string  | null: false |
| card_id     | string  | null: false |

### Association
- belongs_to :user


## categoryテーブル
|Column|Type|Options|
|------|----|-------|
| name     | string | null: false |
| ancestry | string ||

### Association
- has_many :products


## productテーブル

|Column|Type|Options|
|------|----|-------|
| name          | string  | null: false |
| price         | string  | null: false |
| description   | string  | null: false |
| status        | string  | null: false |
| size          | string  | null: false |
| shipping_cost | string  | null: false |
| shipping_days | string  | null: false |
| prefecture_id | string  | null: false |
| judgment      | string  ||
| category_id   | integer | null: false, foreign_key: true |
| brand_id      | integer | null: false, foreign_key: true |
| shipping_id   | integer | null: false, foreign_key: true |
| user_id       | integer | null: false, foreign_key: true |

### Association
- belongs_to :user       dependent: :destroy
- belongs_to :category   dependent: :destroy
- belongs_to :brand      dependent: :destroy
- has_many   :images     dependent: :destroy

- belongs_to_active_hash :prefecture


## imageテーブル
|Column|Type|Options|
|------|----|-------|
| image      | string  | null: false |
| product_id | integer | null: false, foreign_key: true |

### Association
- belongs_to :product


## brandテーブル
|Column|Type|Options|
|------|----|-------|
| name | string | index: true |

### Association
- has_many :products
