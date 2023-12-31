# Laravel Toリスト

## Laravel Sail
参考: https://chigusa-web.com/blog/laravel-sail/
### 1. プロジェクトフォルダの作成
``` sh
cd ~
mkdir フォルダ名
cd フォルダ名
```

### 2. プロジェクトの作成
``` sh
curl -s https://laravel.build/プロジェクト名 | bash
```

### 3. Laravel Sailの起動
``` sh
cd example-app
./vendor/bin/sail up
```

http://localhost/ へアクセス


プロジェクト直下でsailコマンドを実行するために.bashrcに追記
``` sh
vi ~/.bashrc
```

一番最後の行に追記

``` sh
alias sail='[ -f sail ] && bash sail || bash vendor/bin/sail'
```

反映
``` sh
$ source ~/.bashrc
```

``` sh
sail up
```

### 4. phpMyAdminのインストール
docker-compose.ymlに以下の内容を追記
``` yml
phpmyadmin:
    image: phpmyadmin/phpmyadmin
    links:
        - mysql:mysql
    ports:
        - 8080:80
    environment:
        #PMA_USER: "${DB_USERNAME}"
        #PMA_PASSWORD: "${DB_PASSWORD}"
        PMA_HOST: mysql
    networks:
        - sail
```
sailの起動
``` sh
sail up
```
phpMyAdminへアクセス

http://localhost:8080/

.env内のユーザー名、パスワードでログイン
``` env
DB_USERNAME=sail
DB_PASSWORD=password
```

## Laravel
参考: https://b-risk.jp/blog/2022/08/laravel/#PHP

### 1. 日本仕様への変更
config/app.php の内容変更
``` php
'timezone' => 'Asia/Tokyo',
'locale' => 'ja', 
'fallback_locale' => 'ja',
'faker_locale' => 'ja_JP',
```

### 2. APP_NAMEの変更
``` env
APP_NAME=アプリ名
```
タイトルタグなどで以下のようにすると参照できる
``` php
<title>{{ config('app.name') }}</title>
```
