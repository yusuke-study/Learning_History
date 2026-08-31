#	Azure File Sync (ストレージ同期サービス)
 
Azure File Syncとは、オンプレミスのファイルサーバーとAzureのクラウドストレージであるAzure Filesを同期させることで、ファイル共有を効率化するサービスである。 

SMB、NFS、FTPSなどWindows Server上で利用できるあらゆるプロトコルを使用して、アクセスすることができる。

Azure File Syncの構造は下記の通りである。

ストレージ同期サービス（Azure File Sync）

└── 同期グループ（Sync Group）

    ├── クラウドエンドポイント（Cloud Endpoint） ← Azure Files（ファイル共有）
    
    └── サーバーエンドポイント（Server Endpoint） ← オンプレミスのフォルダ

Azure File Syncの設定方法について、コマンドとGUIでの操作方法を下記に記載する。

##	コマンド操作

(1)	ストレージ同期サービス(Azure File Sync)を作成する。

下記コマンドを実行する。

az storagesync create --resource-group <リソースグループ名> --name <ストレージ同期サービス名> --location <リージョン>
 

(2)	同期グループを作成する。

下記コマンドを実行する。

az storagesync sync-group create --resource-group <リソースグループ名> --storage-sync-service <ストレージ同期サービス名> --name <Sync Group名>
 

 

(3)	Azure File Sync にストレージアカウントを読み取らせるロールの付与を行う。※必要な場合

下記コマンドを実行する。

az role assignment create --assignee <Azure File Sync のマネージド ID またはユーザー ID> --role "Storage Account Contributor" --scope /subscriptions/<サブスクリプションID>/resourceGroups/<リソースグループ名>/providers/Microsoft.Storage/storageAccounts/<ストレージアカウント名>
 

 

(4)	クラウドエンドポイントを作成する。

※Azure File SyncのSync GroupにAzureファイル共有を紐付ける操作

下記コマンドを実行する。

az storagesync sync-group cloud-endpoint create --resource-group <リソースグループ名> --storage-sync-service <ストレージ同期サービス名> --sync-group-name <Sync Group 名> --name <Cloud Endpoint名>　--storage-account <ストレージアカウント名> --azure-file-share-name <ファイル共有名>

※--name <Cloud Endpoint名>はどこに反映されるか不明だが、実行しないとエラーになるので実行する。

※削除時に必要になる。
 

 

(5)	Windows　serverに、「Storage Sync Agent」をインストールする。

※GUI操作参照

(6)	登録済みのサーバー一覧を取得する。

下記コマンドを実行する。

az storagesync registered-server list --resource-group <リソースグループ名> --storage-sync-service <ストレージ同期サービス名>　--query "[].{ServerName:serverName, ID:serverId, OS:serverOSVersion}" --output table
 

(7)	サーバーエンドポイントを作成する。

下記コマンドを実行する。

az storagesync sync-group server-endpoint create --resource-group <リソースグループ名> --storage-sync-service <ストレージ同期サービス名> --sync-group-name <Sync Group 名> --name <Server Endpoint 名>　--server-id <登録済みサーバーのID> --server-local-path <同期するローカルフォルダのパス>  [--cloud-tiering true|false]

例：

az storagesync sync-group server-endpoint create --resource-group testResourceGroup_02 --storage-sync-service test-storagesync --sync-group-name test-storagesync-group  --name test-ServerEndpoint --server-id 93a2b931-f233-4b7b-a19e-03b7c33a5909 --server-local-path F:\SyncFolder --cloud-tiering on
 

 

 

(8)	サーバーエンドポイントを削除する。

下記コマンドを実行する。

az storagesync sync-group server-endpoint delete --resource-group <リソースグループ名> --storage-sync-service <ストレージ同期サービス名> --sync-group-name <Sync Group 名> --name <Server Endpoint 名>

例：

az storagesync sync-group server-endpoint delete --resource-group testResourceGroup_02 --storage-sync-service test-storagesync --sync-group-name test-storagesync-group --name test-ServerEndpoint
 

(9)	クラウドエンドポイントを削除する。

下記コマンドを実行する。

az storagesync sync-group cloud-endpoint delete --resource-group <リソースグループ名> --storage-sync-service <ストレージ同期サービス名> --sync-group-name <Sync Group 名> --name <Cloud Endpoint 名>

例：

az storagesync sync-group cloud-endpoint delete --resource-group testResourceGroup_02 --storage-sync-service test-storagesync --sync-group-name test-storagesync-group --name test-CloudEndpoint
 

 

(10)同期グループを削除する。

下記コマンドを実行する。

az storagesync sync-group delete --resource-group <リソースグループ名> --storage-sync-service <ストレージ同期サービス名> --name <Sync Group 名>
 

(11)登録済みサーバーを登録解除する。

下記コマンドを実行する。

az storagesync registered-server delete --resource-group <リソースグループ名> --storage-sync-service <ストレージ同期サービス名> --server-id <登録済みサーバーのID>
 

(12)ストレージ同期サービスを削除する。

下記コマンドを実行する。

az storagesync delete --resource-group <リソースグループ名> --name <ストレージ同期サービス名>
 
 
3.4.2.2	GUI操作

(1)	ストレージ同期サービス(Azure File Sync)を作成する。
 

(2)	オンプレ環境のWindows serverにインストールするための、「Azure File Sync エージェント」を下記URLからダウンロードする。

URL: https://www.microsoft.com/en-us/download/details.aspx?id=57159

※Windows serverのバージョンに合ったものをDLする。

  

(3)	Windows serverに、「Storage Sync Agent」をインストールする。

※Windows serverのバージョンが合っていないとエラーになる。

※Internet Explorer セキュリティ強化の構成をオフにしないと、Microsoftアカウントにブラウザでログインできないことがある。

 　　 

 　　 

(4)	インストール後にAzure Filesとサーバーを同期するための設定を行う。
     　　

 

(5)	同期されると、「登録済みサーバー」が表示される。
 

(6)	同期グループを作成する。
 

(7)	クラウドエンドポイントとサーバーエンドポイントを作成する。

※クラウド階層化はCドライブでは実行できないので、サーバーエンドポイントの追加は別ドライブを作成後に行う。

※ファイルの同期のみであれば、Cドライブでも可能である。
 

 

(8)	サーバーエンドポイントの正常性が「正常」に変化したら作業完了である。

※正常に変化するまで数分かかる。
 

 
3.4.2.3	帯域制限

Azure File Sync帯域制限について下記に記載する。

※Azure File Sync帯域制限を行いたい場合、コマンドのみで実行確認である。

※Storage Sync Agentを入れたサーバーでコマンドを実行する。


(1)	下記コマンドでモジュールのインストールを行う。

Import-Module “C:\Program Files\Azure\StorageSyncAgent\StorageSync.Management.ServerCmdlets.dll"

(2)	下記コマンドでモジュールの確認を行う。

Get-StorageSyncNetworkLimit

Get-StorageSyncNetworkLimit # assumes StorageSync.Management.ServerCmdlets.dll is imported

例）月～金 9:00-18:00は100Mbpsを上限とする場合は下記を実行する。

New-StorageSyncNetworkLimit -Day Monday, Tuesday, Wednesday, Thursday, Friday -StartHour 9 -EndHour 18 -LimitKbps 100000

ネットワークの制限を削除する場合(全て)は下記を実行する。

Get-StorageSyncNetworkLimit | ForEach-Object { Remove-StorageSyncNetworkLimit -Id $_.Id } # assumes StorageSync.Management.ServerCmdlets.dll is imported


クラウド階層化の設定

クラウドを使った階層化とは、名前空間 (ファイルとフォルダーの階層、およびファイルのプロパティ) とファイルコンテンツを分離することである。

 




クラウドを使った階層化のポリシー

「ボリュームの空き領域ポリシー」および「日付ポリシー」 の2つのポリシーがある。

・ボリュームの空き領域ポリシー

ローカル ディスク上で一定の容量が使用されている場合に、クールファイルをクラウドに階層化するように Azure File Sync に指示を行う。

・日付ポリシー

x 日間アクセスされていない (読み書きされていない) クール ファイルがクラウドに階層化される。

 


 


階層化されたファイル

階層化されたファイルは、ファイルのコンテンツ自体がローカルに保存されていないため、ディスク上のサイズはゼロになる。 

ファイルが階層化されると、Azure File Sync ファイル システム フィルター (StorageSync.sys) によって、ローカルでファイルが再解析ポイントと呼ばれるポインターと置き換えられる。

 

ローカルにキャッシュされたファイル

オンプレミスのファイル サーバーに格納されているファイルの場合、ファイル全体 (ファイル属性とファイル コンテンツ) はローカルに保存されるため、ディスク上のサイズはファイルの論理サイズとほぼ同じになる。

 


Azure Files と Azure File Sync に Azure プライベート エンドポイントを実装することにより、パブリック エンドポイント アクセスは無効になり、Azure 仮想ネットワークからの Azure Files と Azure File Sync へのアクセスが制限される。


Azure File Sync のパブリック ドメイン名 *.afs.azure.net は、CNAME リダイレクトによってプライベート ドメイン名 *.<region>.privatelink.afs.azure.net になる。

Azure Files のパブリック ドメイン名 <name>.file.core.windows.net は、CNAME リダイレクトによってプライベート ドメイン名 <name>.privatelink.file.core.windows.net になる。



