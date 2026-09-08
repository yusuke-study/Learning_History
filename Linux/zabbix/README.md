# Zabbix 画面

![zabbix](./zabbix_01.png)

![zabbix](./zabbix_02.png)

![zabbix](./zabbix_03.png)

![zabbix](./zabbix_04.png)

##	Zabbix 設定ファイル　etc

設定ファイル：/etc/zabbix/zabbix_server.conf

※設定の主なポイント　※要件によって違うため、主要な重要部分のみ解説

① MySQLへの接続設定を追加する。「DBPassword=password」

![zabbix](./zabbix_05.png)

② SNMPTrapperFileのログを設定する場合に記載する。　例：「SNMPTrapperFile=」

![zabbix](./zabbix_06.png)

③ SNMP Trap を取り込む機能を有効化する。「StartSNMPTrapper=1」

![zabbix](./zabbix_07.png)

④ スクリプト実行権限を有効化する際に設定する。「EnableGlobalScripts=1」

![zabbix](./zabbix_08.png)

※スクリプト参考例

![zabbix](./zabbix_09.png)

##	snmptrapd 設定ファイル　etc

設定ファイル：/etc/snmp/snmptrapd.conf

![zabbix](./zabbix_10.png)  


##	snmptrapdログ設定

EDITOR=vi systemctl edit snmptrapdで編集する

![zabbix](./zabbix_11.png)  


