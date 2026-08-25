#S3



##S3コマンド操作

主に使用する汎用バケットについてのコマンド操作を下記に記載する。

(1)	汎用バケットを作成する。

「aws s3api create-bucket --bucket <バケット名> --region ap-northeast-1 --create-bucket-configuration LocationConstraint=ap-northeast-1」を実行する。

※その他のオプション例：

--acl：アクセス制御（例：private, public-read） 

--object-lock-enabled-for-bucket：オブジェクトロックの有効化

 

(2)	汎用バケットを一覧表示する。
「aws s3api list-buckets --query "Buckets[*].Name" --output text」を実行する。
 

(3)	汎用バケットを削除する。
「aws s3api delete-bucket --bucket  <バケット名>」を実行する。
 

(4)	汎用バケット内にファイルをアップロードする。
「aws s3 cp <ローカルのファイル名> s3://<バケット名>/<ファイル名>」を実行する。
 

 

(5)	パブリックアクセスブロックの解除を設定する。
「aws s3api delete-public-access-block --bucket <バケット名>」を実行する。
 
実行結果：
