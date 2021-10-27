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
```