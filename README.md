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

