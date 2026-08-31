Azure File(ストレージ アカウント)の設定方法について、ファイル構造、コマンドとGUIでの操作方法を下記に記載する。

3.4.1.1	ファイル構造
ストレージアカウントには、下記の4種類が存在するが、下記にその構造と特徴を記載する。

ストレージアカウント
└── コンテナ（Container）
│  ├── Blob（ファイル）1
│  ├── Blob（ファイル）2
└── ファイル共有（File Share）
│   ├── フォルダ1
│   │   ├── ファイルA
│   │   └── ファイルB
│   └── フォルダ2
└── Queue
└── Table

(1)	Blob コンテナの構成（Blob Storage）
Blob ストレージは、オブジェクトストレージであり、画像、動画、ドキュメントなどを保存する。

(2)	ファイル共有の構成（Azure Files）
Azure Files は、Windowsの共有フォルダのような階層型ファイルシステムであり、ネットワークドライブとしてSMBプロトコルでマウント可能である。(Azure File Sync)
（WindowsやLinuxから \\storageaccount.file.core.windows.net\<sharename> でアクセス可能となる。）

(3)	Queue
メッセージの一時保存と処理に利用され、メッセージはFIFO（先入れ先出し）で処理される。

(4)	Table
NoSQL型のキーバリューストアである。高速な読み書きが可能であり、ログや監査情報の保存に使用され、クエリで柔軟に検索が可能である。
 
3.4.1.2	コマンド操作

(1)	ストレージアカウントを作成する。
下記コマンドを実行する。
az storage account create --name <ストレージアカウント名> --resource-group <リソースグループ名> --location <リージョン> --sku <SKUタイプ> --kind <ストレージアカウントの種類>

※<ストレージアカウント名>は、一意の名前である必要有
※--skuは、下記から選択する。




※--kindは、下記から選択する。




例①：
az storage account create --name teststorage20251020 --resource-group testResourceGroup_02 --location japaneast --sku Standard_LRS --kind StorageV2
