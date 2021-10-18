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
```
