# fleamarket_sample_79c DB設計
## usersテーブル
|Column|Type|Option|
|------|----|------|
|nickname|string|null: false|
|email|string|null: false, unique: true|
|password|string|null: false|
|first_name|string|null: false|
|last_name|string|null: false|
|birth_day|integer|null: false|
|birth_month|integer|null: false|
|birth_year|integer|null: false|
|first_name_kana|string|null: false|
|last_name_kana|string|null: false|
|phone_number|string||
### Association
- has_one :address, dependent: :destroy
- has_one :card, dependent: :destroy
- has_many :posts, dependent: :destroy
- has_many :likes, dependent: :destroy
- has_many :liked_posts, through: :likes, source: :post
- has_many :comments
- has_many :sns_credentials

## addressesテーブル
|Column|Type|Option|
|------|----|------|
|postal_code|string|null: false|
|prefecture|integer|null: false|
|city|string|null: false|
|address|string|null: false|
|apartment|string||
|user|references|null: false, foreign_key: true|
### Association
- belongs_to :user

## cardsテーブル
|Column|Type|Option|
|------|----|------|
|customer_id|string|null: false|
|user|references|null: false, foreign_key: true|
|card_id|string|null: false|
### Association
- belongs_to :user

## postsテーブル
|Column|Type|Option|
|------|----|------|
|name|string|null: false, add_index: true|
|text|text|null: false|
|condition|integer|null: false|
|burden|integer|null: false|
|area|integer|null: false|
|day|integer|null: false|
|price|string|null: false|
|user|references|null: false, foreign_key: true|
|category|references|null: false, foreign_key: true|
|brand|string|null: false|
|buyer_id|integer||
### Association
- belongs_to :user dependent: :destroy
- belongs_to :category dependent: :destroy
- has_many :images dependent: :destroy
- has_many :likes
- has_many :liked_users, through: :likes, source: :user
- has_many :comments

## categoriesテーブル
|Column|Type|Option|
|------|----|------|
|name|string|null: false|
|ancestry|string|null: false|
### Association
- has_many :posts

## imagesテーブル
|Column|Type|Option|
|------|----|------|
|name|string|null: false|
|post|references|null: false, foreign_key: true|
### Association
- belongs_to :post 

## commentsテーブル
|Column|Type|Option|
|------|----|------|
|user_id|integer||
|post_id|integer||
|content|text||

### Association
- belongs_to :post
- belongs_to :user


## likessテーブル
|Column|Type|Option|
|------|----|------|
|post|references|null: false|
|user|references|null: false|

### Association
- belongs_to :user
- belongs_to :post 
