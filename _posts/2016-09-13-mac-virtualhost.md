# Macでバーチャルホストを構築してテスト環境

## httpd.confを編集

Apache2のconfigを書き換えて、バーチャルホストを有効にする。

`$ sudo vi /etc/apache2/httpd.conf`

下記の行のコメントを外す

```
# Virtual hosts
Include /private/etc/apache2/extra/httpd-vhosts.conf
```
## バーチャルホストのconfigを編集

バーチャルホストの設定を追加する。

`$ sudo vi /private/etc/apache2/extra/httpd-vhosts.conf`

下記のブロックを追加する

```
<VirtualHost *:80>
    ServerAdmin webmaster@local.example.com
    DocumentRoot "/usr/docs/local.example.com"
    ServerName local.example.com
    ServerAlias www.local.example.com
    ErrorLog "/private/var/log/apache2/local.example.com-error_log"
    CustomLog "/private/var/log/apache2/local.example.com-access_log" common
</VirtualHost>
```

## hostsファイルの編集

バーチャルホストとして追加したドメインにアクセスした時に、ローカルアクセスとなるように設定を追加する。

`$ sudo vi /etc/hosts`

下記行を追加する

```
127.0.0.1    local.example.com
```

## Apacheの再起動

configが正しく読み込めるかチェックする

`$ apachectl -t`

パスの書き間違いなどがあれば下記のように表示される

```
AH00112: Warning: DocumentRoot [/usr/docs/local.example.com] does not exist
AH00112: Warning: DocumentRoot [/usr/docs/local2.example.com] does not exist
Syntax OK
```

問題がなければ下記のように表示

`Syntax OK`

sudoで再起動を実行

`$ sudo apachectl restart`

## シンボリックリンクを作成する

シンボリックリンクの元となるバーチャルホスト側のディレクトリを作成する

`$ sudo mkdir /usr/docs/local.example.com`

ワークスペースにシンボリックリンクを作成する

`$ ln -s /usr/docs/local.example.com ~/work/local.example.com`

lsで確認すると、下記のように表示される

```
$ ls -ltr
total 2
lrwxr-xr-x   1 user  staff   45 Sep 13 12:16 local.example.com -> /usr/docs/local.example.com
```

## ブラウザで確認

index.htmlを作成し、ブラウザで表示できるか確認する

`vi index.html`

`hello.`

http://local.example.com

![browser_check](https://github.com/kenta-fujiwara/kenta-fujiwara.github.io/blob/master/images/browser_check.png)
