### self-join ###

Practising self association/ self-join tables in Rails.

```
rails new self-join -d postgresql
cd self-join/
rails db:create
rails db:migrate

rails g scaffold user name:string
rails db:migrate

rails g model Follow follower_id:integer followee_id:integer

code .
to Follow model:
class Follow < ApplicationRecord
  belongs_to :follower, class_name: 'User'
  belongs_to :followee, class_name: 'User'
end

to User model:
class User < ApplicationRecord
  has_many :followed_users, foreign_key: :follower_id, class_name: 'Follow'
  has_many :followees, through: :followed_users

  has_many :following_users, foreign_key: :followee_id, class_name: 'Follow'
  has_many :followers, through: :following_users
end

rails db:migrate

User.create(name: "User1")
User.create(name: "User2")
User.create(name: "User3")

user1 = User.first
user2 = User.second

user1.followers << user2
[resource1].followees << [resource2]

view associations:
[resource].followers
[resource].followees

```

ref https://medium.com/@TheDickWard/self-referential-relationships-aka-self-joins-in-rails-64f8f36ac311
