## Web前提条件

Webサイトは、Windows server上に、Apache ＋ Tomcatをインストールした状態とする。

Webサーバーとして機能するために、追加でJAVAをインストールする。

## JAVAインストール

![nr](./nr_01.png)

![nr](./nr_02.png)

![nr](./nr_03.png)

![nr](./nr_04.png)

環境変数の設定を追加する。　「JAVA_HOME」

![nr](./nr_05.png)

![nr](./nr_06.png)

![nr](./nr_07.png)

![nr](./nr_08.png)

## Apache ＋ Tomcatインストール

![nr](./nr_09.png)

![nr](./nr_10.png)

![nr](./nr_11.png)

「services.msc」でサービスを起動し、Apache Tomcatを自動起動に切り替え

![nr](./nr_12.png)

下記コマンドでFirewall（ファイアウォール）の設定を行う

New-NetFirewallRule -DisplayName "Tomcat8080" -Direction Inbound -Protocol TCP -LocalPort 8080 -Action Allow

![nr](./nr_13.png)

## Webサーバー構成

Webサーバーに必要な設定は下記とする

![nr](./nr_14.png)

redisson.yaml

![nr](./nr_15.png)

confcontext.xml

![nr](./nr_16.png)

context.xml

![nr](./nr_17.png)


lib配下には、下記ファイルをインストールしてきて配置する。

![nr](./nr_18.png)


webapps配下にWebの設定ファイルを配置する


