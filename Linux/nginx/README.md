#	nginx

##	nginx 設定ファイル　etc

設定ファイル：/etc/redis/redis.conf

※設定の主なポイント　※要件によって違うため、主要な重要部分のみ解説

①bind設定は、既存の「bind 127.0.0.1 -::1」をコメントアウトし、「bind 0.0.0.0」等を追加する。

セキュリティを気にする場合は、「bind 127.0.0.1 192.168.xx.xx」のように、localhostと、自IPのみ接続許可する

![rs](./redis_01.png)

②「masterauth "foobared"」のコメントアウトを外す

![rs](./redis_02.png)




##	インストール　etc
