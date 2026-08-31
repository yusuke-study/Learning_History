#	別プロバイダーストレージ検証

##	AWS、Azure共通のストレージ一元管理システム

別プロバイダーのシステムと連携し、ストレージ等のデータを一元管理することができるCloud Volumes ONTAPについて、下記に記載する。

##	Cloud Volumes ONTAP

Cloud Volumes ONTAP（以下、CVO）は、NetAppのストレージに搭載されているストレージ専用OSであるONTAPをパブリッククラウド（AWS、Azure、Google Cloud）のIaaS上にデプロイすることができるサービスである。

NetAppのストレージサービスを一元管理すること、NetAppが提供する様々なデータ管理サービスを利用することができるSaaS型のコントロールプレーンとして、NetApp Blue XPというサービスがある。

Blue XP自体は無償で利用することができ、Blue XP Connectorという管理用のコンポーネントはVM上で稼働する。


構成イメージ #下記の画面は全て2025年時点のものであり、2026年以降は変更済の可能性有

![CVO](./CVO_01.png)
 
##	Connector作成 

Blue XP Connector(仮想マシン)の作成手順は以下の通りである。

(1)	NetApp BlueXPポータル画面から、Connectorの設定を行う。

![CVO](./CVO_02.png)

(2)	プロバイダーの選択を行う。

![CVO](./CVO_03.png)

(3)	各種設定を行う。

AWSの設定例：

Access keyとsecret access key情報を入力し、VPC.サブネット等の設定を選択する。

※作成済みの場合に限る。

![CVO](./CVO_04.png) 

![CVO](./CVO_05.png)
 

Azureの設定例：

NetApp Blue XPポータル上からAzureにログインし、リソースグループ、仮想ネットワークの選択を行う。

※作成済みの場合に限る。
 
![CVO](./CVO_06.png)
 
![CVO](./CVO_07.png)

(4)	設定が完了する。
 　　　 
![CVO](./CVO_08.png)

![CVO](./CVO_09.png) 

![CVO](./CVO_10.png)

![CVO](./CVO_11.png) 

 
##	CVO作成 

NetApp Blue XPを使って、Cloud Volumes ONTAPを作成する手順は大まかに以下の通りである。(画面はAWSでの作成)

(1)	Blue XPコンソールを操作し、AWS marketplaceからNetApp Blue XPをSubscribeする。
 
![CVO](./CVO_12.png) 
 
![CVO](./CVO_13.png) 

![CVO](./CVO_14.png) 

![CVO](./CVO_15.png) 
 

(2)	Blue XPコンソールを操作し、Cloud Volumes ONTAP (CVO)を作成、各種情報を入力＆選択する。
 
![CVO](./CVO_16.png) 
 
![CVO](./CVO_17.png) 

![CVO](./CVO_18.png)  

![CVO](./CVO_19.png) 

![CVO](./CVO_20.png) 

(3)	AWSのS3に空のbucketが作成される。

![CVO](./CVO_21.png) 

(4)	Blue XPコンソール上に、CVOとS3が表示される。

![CVO](./CVO_22.png) 
 
##	CVO作成後のAzureステータス等 

※下記はAzureでCloud Volumes ONTAP　（CVO）作成後の画面である。(作業省略)

CVOデプロイまで約30～40分程度かかる。

![CVO](./CVO_23.png)  

![CVO](./CVO_24.png)   

![CVO](./CVO_25.png)                            

![CVO](./CVO_26.png)


数分したら自然と連携される。

Azure上にストレージが3つ作成される。
 　　　　  
![CVO](./CVO_27.png)
 
![CVO](./CVO_28.png)

![CVO](./CVO_29.png) 

![CVO](./CVO_30.png)

## Azure Blobからバックアップ 

●Azure Blobから、CVOにバックアップを行う際の大まかな手順は以下の通りである。

(1)	データブロッカーを作成する。

※データブロッカーとは？主な用途は下記の通りである。

•	データアクセスの制御

o	データブロッカーは、特定のデータセットへの不正アクセスを防ぐために使用される。

o	サービスプロバイダーやシステム管理者が特定のデータを操作・閲覧することを制限するための機能を用いる。

•	リージョン間のデータ移動制限

o	データの地理的制限（データ主権）を遵守するため、データが特定の地域外に転送されることを防ぐ役割を果たす。

![CVO](./CVO_31.png)
 

(2)	指定先のファイルやディレクトリーの指定、バックアップ時間の指定等を行う。
 
![CVO](./CVO_32.png)

![CVO](./CVO_33.png)

(3)	ファイルの同期設定が完成する。

![CVO](./CVO_34.png)
 
![CVO](./CVO_35.png)
 


オンプレONTAPの2次バックアップ先にCVOを想定した場合の構成は下記の通りである。

![CVO](./CVO_36.png)
