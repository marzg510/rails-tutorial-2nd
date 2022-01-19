https://railstutorial.jp/chapters/beginning?version=6.0#cha-beginning

1.2.2Railsをインストールする
echo "gem: --no-document" >> ~/.gemrc
gem install rails -v 6.0.3
rails -v


Yarnインストール
https://classic.yarnpkg.com/en/docs/install/#debian-stable

sudo npm install --global yarn
yarn --version


1.3最初のアプリケーション
mkdir environment
cd environment/
sudo apt-get install libsqlite3-dev
gem install sqlite3 -v '1.4.2' --source 'https://rubygems.org/'
yarn install --check-files
rails webpacker:install
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.0/install.sh | bash
nvm install v12.16.3
rails _6.0.3_ new hello_app

1.3.1Bundler

``` bash
cd hello_app/
bundle install
```

1.3.2rails server

``` bash
cd hello_app/
rails server

```

http://localhost:3000/

1.3.4Hello, world!

- Applicationコントローラにhelloを追加する
- ルートルーティングを設定する

1.5デプロイする

Gemfile
本番用以外のgemをインストールする

``` bash
bundle install --without production
```

git commit


``` bash
sudo snap install --classic heroku
heroku --version
heroku login --interactive
heroku create rails-tutorial-2nd-m510
git add -A
git commit -m "heroku create"
git push heroku master
```


2.1アプリケーションの計画

``` bash
rails _6.0.3_ new toy_app
bundle install --without production
```

``` bash
heroku create toy-app-m510
git push heroku master
```

2.2Usersリソース

``` bash
rails generate scaffold User name:string email:string
rails db:migrate
```

2.3Micropostsリソース

``` bash
rails genarate scaffold Micropost content:text user_id:integer
rails db:migrate
```


2.3.3ユーザーはたくさんマイクロポストを持っている

``` bash
```


2.3.5アプリケーションをデプロイする

``` bash
git commit
git push heroku
heroku logs
heroku run rails db:migrate
```

# 第3章 ほぼ静的なページの作成

3.1セットアップ

``` bash
rails _6.0.3_ new sample_app
cd sample_app
bundle install --without production

```

3.2.1静的なページの生成


``` bash
rails generate controller StaticPages home help

```

- 演習

``` bash
rails generate controller Foo bar baz

rails destroy  controller Foo bar baz


```

3.3.1最初のテスト

``` bash
rails db:migrate

rails test

```

3.6.2Guardによるテストの自動化

``` bash
bundle exec guard init   # Guardfileサンプル生成

bundle exec guard

```

# 第4章 Rails風味のRuby

## 4.1動機

``` bash
git checkout -b rails-flavored-ruby

```

## 4.2文字列とメソッド

### 4.2.1

- 演習

``` ruby
# 1
city = "蕨"
prefecture = "埼玉"
# 2
puts "#{prefecture}県 #{city}市"
# 3
puts "#{prefecture}県	#{city}市"
#4
puts '#{prefecture}県	#{city}市'

```

### 4.2.2

- 演習

``` ruby
# 1
"racecar".length
# 2
"racecar".reverse
# 3
s = "racecar"
s = s.reverse
# 4
puts "It's a palindrome!" if s == s.reverse

```

### 4.2.3メソッドの定義

- 演習

``` ruby
#1
def palindrome_tester(s)
  if s == s.reverse
    puts "It's a palindrome!"
  else
    puts "It's not a palindrome."
  end
end

#2
>> palindrome_tester("racecar")
It's a palindrome!
=> nil
>> palindrome_tester("onomatopoeia")
It's not a palindrome.
=> nil

#3
palindrome_tester("racecar").nil?

```

### 4.2.4titleヘルパー、再び

### 4.3他のデータ構造

- 演習

``` ruby
#1
a = "A man,a plan,a canal, Panama".split(',')

#2
a = a.join

#3
('a'..'z').to_a[7]
('a'..'z').to_a[-7]

```

### 4.3.2ブロック

- 演習

``` ruby
#1
(0..16).map { |i| i ** 2 }

#2
>> def yeller(s)
>>   s.map { |c| c.upcase }.join
>> end
=> :yeller
>> yeller(%w[o l d])
=> "OLD"

#3
>> def random_subdomain
>>   ('a'..'z').to_a.shuffle[0..7].join
>> end
=> :random_subdomain
>> random_subdomain
=> "uzmokfnq"

#4
>> def string_shuffle(s)
>>   s.split('').shuffle.join
>> end
=> :string_shuffle
>> string_shuffle("foobar")
=> "oforba"

```


### 4.3.3ハッシュとシンボル

- 演習

``` ruby
#1
h = { 'one' => 'uno', 'two' => 'dos', 'three' => 'tres' }
h.each do |key,value|
  puts "'#{key}'はスペイン語で'#{value}'"
end

#2
person1 = { :first => 'm', :last => 'g' }
person2 = { :first => 'm2', :last => 'g2' }
person3 = { :first => 'm3', :last => 'g3' }

params[:father] = person1
params[:mother] = person2
params[:child] = person3

params[:father][:first] == person1[:first]
params[:father][:last] == person1[:last]
params[:mother][:first] == person2[:first]
params[:mother][:last] == person2[:last]
params[:child][:first] == person3[:first]
params[:child][:last] == person3[:last]

#3
user = { :name => 'm', :email => 'g', :password_digest => ('a'..'z').to_a.shuffle[0..15].join }

#4
{ "a" => 100, "b" => 200 }.merge({ "b" => 300 })
=> {"a"=>100, "b"=>300}


```

## 4.4Rubyにおけるクラス

### 4.4.1コンストラクタ

- 演習

``` ruby
#1

(1..10)

#2

Range.new(1,10)

#3

>> (1..10) == Range.new(1,10)
=> true

```

### 4.4.2クラス継承

- 演習

``` ruby
#1
>> Range.class.superclass
=> Module
>> Range.class.superclass.superclass
=> Object
>> Hash.class.superclass
=> Module
>> Hash.class.superclass.superclass
=> Object
>> Symbol.class.superclass
=> Module

#2
>> class Word2 < String
>>   def palindrome?
>>     self == reverse
>>   end
>> end

```


### 4.4.3組み込みクラスの変更

- 演習

``` ruby
#1
"racecar".palindrome?

#2
class String
  def shuffle
    self.split('').shuffle.join
  end
end
"test".shuffle

#3
class String
  def shuffle
    split('').shuffle.join
  end
end
"test".shuffle

```

### 4.4.4コントローラクラス

- 演習

``` ruby
#1
>> user = User.new
=> #<User id: nil, name: nil, email: nil, created_at: nil, updated_at: nil>

#2
>> user.class
=> User(id: integer, name: string, email: string, created_at: datetime, updated_at: datetime)
>> user.class.superclass
=> ApplicationRecord(abstract)
>> user.class.superclass.superclass
=> ActiveRecord::Base
>> user.class.superclass.superclass.superclass
=> Object

```

### 4.4.5ユーザークラス

## 4.5最後に

```bash
git commit -am "Add a full_title helper"
git checkout main
git merge rails-favored-ruby

```

# 第5章 レイアウトを作成する

## 5.1構造を追加する

```bash
git checkout -b filling-in-layout
```

- 演習

``` ruby
# 1
curl -OL https://cdn.learnenough.com/kitten.jpg
```

### 5.1.2BootstrapとカスタムCSS

## 5.2Sassとアセットパイプライン

## 5.3レイアウトのリンク

### 5.3.3名前付きルート

### 5.3.4リンクのテスト

## 5.4ユーザー登録: 最初のステップ

### 5.4.1Usersコントローラ

```bash
rails generate controller Users new

```

### 5.4.2ユーザー登録用URL

演習

```bash

```

# 第6章 ユーザーのモデルを作成する

## 6.1 Userモデル

### 6.1.1データベースの移行

### 6.1.4ユーザーオブジェクトを検索する

### 6.1.5 ユーザーオブジェクトを更新する

## 6.2ユーザーを検証する

### 6.2.1有効性を検証する


``` bash
rails test:models
```

#### 演習

``` ruby
u = User.new()
u.valid?
u.errors.messages[:email]
```

``` shell
rails generate migration add_index_to_users_email
```

### 6.2.5 一意性を検証する

#### 演習

``` ruby
```

## 6.3セキュアなパスワードを追加する

### 6.3.1ハッシュ化されたパスワード

### 6.3.2ユーザーがセキュアなパスワードを持っている

#### 演習

``` ruby
>> user = User.new(name: "test", email:"test@test.com")
   (0.2ms)  begin transaction
=> #<User id: nil, name: "test", email: "test@test.com", created_at: nil, updated_at: nil, password_digest: nil>
>> user.valid?
  User Exists? (0.4ms)  SELECT 1 AS one FROM "users" WHERE LOWER("users"."email") = LOWER(?) LIMIT ?  [["email", "test@test.com"], ["LIMIT", 1]]
=> false
>> 
```

### 6.3.3パスワードの最小文字数

``` ruby
>> user = User.new(name: "test", email:"test@test.com", password:"12345", password_confirmation: "12345")
=> #<User id: nil, name: "test", email: "test@test.com", created_at: nil, updated_at: nil, password_digest: [FILTERED]>
>> user.valid?
  User Exists? (0.3ms)  SELECT 1 AS one FROM "users" WHERE LOWER("users"."email") = LOWER(?) LIMIT ?  [["email", "test@test.com"], ["LIMIT", 1]]
=> false
>> user.errors.full_messages
=> ["Password is too short (minimum is 6 characters)"]
```

### 6.3.4ユーザーの作成と認証

```
>> user.authenticate("not_the_right_password")
=> false
>> user.authenticate("foobar")
=> #<User id: 1, name: "Micael Hartl", email: "michael@example.com", created_at: "2021-12-15 09:45:36", updated_at: "2021-12-15 09:45:36", password_digest: [FILTERED]>
>> user.authenticate("foobaz")
=> false
```


#### 演習

``` ruby
>> user = User.find_by(email:"michael@example.com")
   (1.1ms)  SELECT sqlite_version(*)
  User Load (0.6ms)  SELECT "users".* FROM "users" WHERE "users"."email" = ? LIMIT ?  [["email", "michael@example.com"], ["LIMIT", 1]]
>> user.name = "test"
=> "test"
>> user.save
   (0.1ms)  begin transaction
  User Exists? (0.3ms)  SELECT 1 AS one FROM "users" WHERE LOWER("users"."email") = LOWER(?) AND "users"."id" != ? LIMIT ?  [["email", "michael@example.com"], ["id", 1], ["LIMIT", 1]]
   (0.2ms)  rollback transaction
=> false
>> user.valid?
  User Exists? (0.3ms)  SELECT 1 AS one FROM "users" WHERE LOWER("users"."email") = LOWER(?) AND "users"."id" != ? LIMIT ?  [["email", "michael@example.com"], ["id", 1], ["LIMIT", 1]]
=> false
>> user.errors.full_messages
=> ["Password can't be blank", "Password is too short (minimum is 6 characters)"]
>> user
=> #<User id: 1, name: "test", email: "michael@example.com", created_at: "2021-12-15 09:45:36", updated_at: "2021-12-15 09:45:36", password_digest: [FILTERED]>
>> user.reload
  User Load (0.8ms)  SELECT "users".* FROM "users" WHERE "users"."id" = ? LIMIT ?  [["id", 1], ["LIMIT", 1]]
=> #<User id: 1, name: "Micael Hartl", email: "michael@example.com", created_at: "2021-12-15 09:45:36", updated_at: "2021-12-15 09:45:36", password_digest: [FILTERED]>
>> user.update(name:"test")
   (0.1ms)  begin transaction
  User Exists? (0.3ms)  SELECT 1 AS one FROM "users" WHERE LOWER("users"."email") = LOWER(?) AND "users"."id" != ? LIMIT ?  [["email", "michael@example.com"], ["id", 1], ["LIMIT", 1]]
   (2.5ms)  rollback transaction
=> false
>> user.valid?
  User Exists? (0.3ms)  SELECT 1 AS one FROM "users" WHERE LOWER("users"."email") = LOWER(?) AND "users"."id" != ? LIMIT ?  [["email", "michael@example.com"], ["id", 1], ["LIMIT", 1]]
=> false
>> user.errors.full_messages
=> ["Password can't be blank", "Password is too short (minimum is 6 characters)"]
>> user.reload
  User Load (0.3ms)  SELECT "users".* FROM "users" WHERE "users"."id" = ? LIMIT ?  [["id", 1], ["LIMIT", 1]]
=> #<User id: 1, name: "Micael Hartl", email: "michael@example.com", created_at: "2021-12-15 09:45:36", updated_at: "2021-12-15 09:45:36", password_digest: [FILTERED]>
>> user.update_attribute(:name, "test")
   (0.1ms)  begin transaction
  User Update (4.1ms)  UPDATE "users" SET "name" = ?, "updated_at" = ? WHERE "users"."id" = ?  [["name", "test"], ["updated_at", "2021-12-15 09:57:41.499694"], ["id", 1]]
   (627.6ms)  commit transaction
=> true
>> user.name
=> "test"
>> user.reload
  User Load (0.3ms)  SELECT "users".* FROM "users" WHERE "users"."id" = ? LIMIT ?  [["id", 1], ["LIMIT", 1]]
=> #<User id: 1, name: "test", email: "michael@example.com", created_at: "2021-12-15 09:45:36", updated_at: "2021-12-15 09:57:41", password_digest: [FILTERED]>
>> 
```

# 第7章 ユーザー登録

## 7.1ユーザーを表示する

### 7.1.1デバッグとRails環境

テスト環境
```bash
rails console -e test
```

### 7.1.2Usersリソース

### 7.1.3debuggerメソッド

### 7.1.4Gravatar画像とサイドバー


## 7.2 

### 7.2.2フォームHTML

## 7.3 ユーザー登録失敗

### 7.3.1正しいフォーム