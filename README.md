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

