
インターネットに出られないとき。

![DNS](./DNS_01.png)  

DNSフォワーダー設定を行う。※ping 8.8.8.8が応答する場合

Add-DnsServerForwarder -IPAddress 8.8.8.8

![DNS](./DNS_02.png)  

DNSキャッシュをクリア

Clear-DnsServerCache

![DNS](./DNS_03.png)  

ツール上でも確認

![DNS](./DNS_04.png)  
