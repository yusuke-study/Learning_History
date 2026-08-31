# IAM  ![IAM](./IAM_00.png)

IAMに関連するシステムの確認を行うコマンドについて記載する。

前提条件として、AWS CLIにログインした状態であること。

## IAM ユーザー

IAMユーザーに関連するコマンドを記載する。

(1)	AWSユーザー一覧を表示する。

「aws iam list-users」を実行する。
 
![IAM](./IAM_01.png)

(2)	ユーザー名だけ出力する。

「aws iam list-users `--query` 'Users[].UserName'」を実行する。

![IAM](./IAM_02.png)


(3)	ユーザーを作成する。
「aws iam create-user `--user-name` ユーザー名」を実行する。
 
![IAM](./IAM_03.png)

![IAM](./IAM_04.png)

(4)	アクセスキーを作成する。

「aws iam create-access-key `--user-name` ユーザー名」を実行する。

![IAM](./IAM_05.png)

(5)	パスワードを設定する。

「aws iam create-login-profile `--user-name` ユーザー名 `--password` パスワード `--password-reset-required`」を実行する。

![IAM](./IAM_06.png)

(6)	「パスワードのリセットが必要」設定の反映をする。

「aws iam attach-user-policy `--user-name` ユーザー名 `--policy-arn` arn:aws:iam::aws:policy/IAMUserChangePassword」を実行する。

![IAM](./IAM_07.png)

## IAM グループ

IAMグループに関連するコマンドを記載する。

(1)	グループの一覧を表示する。

「aws iam list-groups」を実行する。

![IAM](./IAM_08.png)

(2)	グループ名だけ出力する。

「aws iam list-groups `--query` 'Groups[].GroupName'」を実行する。

![IAM](./IAM_09.png)

(3)	グループを作成する。

「aws iam create-group `--group-name` グループ名」を実行する。

 ![IAM](./IAM_10.png)

(4)	ユーザーをグループに追加する。

「aws iam add-user-to-group `--user-name` ユーザー名 `--group-name` グループ名」を実行する。

 ![IAM](./IAM_11.png) 

(5)	ユーザーが所属しているグループを表示する。

「aws iam list-groups-for-user `--user-name`　ユーザー名」を実行する。

 ![IAM](./IAM_12.png) 



## IAM ポリシー


IAMポリシーに関連するコマンドを記載する。

(1)	カスタムポリシーのみを一覧表示する。

「aws iam list-policies `--scope` Local」を実行する。

 ![IAM](./IAM_13.png) 

(2)	ユーザーにポリシーを付与する

「aws iam attach-user-policy `--user-name` ユーザー名  `--policy-arn` arn:aws:iam::aws:policy/<ポリシー名>」を実行する。
 
 ![IAM](./IAM_14.png) 
 
 ![IAM](./IAM_15.png) 

(3)	ユーザーにアタッチされているポリシーを表示する。

「aws iam list-attached-user-policies `--user-name` ユーザー名」を実行する。

![IAM](./IAM_16.png) 

(4)	グループにアタッチされているポリシーを表示する。

「aws iam list-attached-group-policies `--group-name` グループ名 」を実行する。
 
![IAM](./IAM_17.png) 

(5)	ポリシーを作成するための内容を定義する。

Jsonファイルを作成する。（例）

EC2のフルアクセス権限

[`EC2-full-access-policy.json ダウンロード`](./EC2-full-access-policy.json)

(6)	ポリシーを作成する。

「aws iam create-policy `--policy-name` ポリシー名 `--policy-document` file://<ファイルパス>」を実行する。
 
![IAM](./IAM_18.png) 

![IAM](./IAM_19.png) 


(7)	ポリシーの内容を表示する。

「aws iam get-policy-version `--policy-arn` arn `--version-id` v1」を実行する。

![IAM](./IAM_20.png) 

※JSON形式のポリシー一例は以下である。

![IAM](./IAM_21.png) 

IAMポリシーの基本構造（JSON）　一例  ※細かく設定する場合

[`ポリシー ダウンロード`](./Detailed policies.json)



## IAM ロール


IAMロールに関連するコマンドを記載する。

(1)	IAMロールの一覧表示をする。

「aws iam list-roles」を実行する。

![IAM](./IAM_22.png)  

(2)	IAMロール名だけ出力する。

「aws iam list-roles  `--query` 'Roles[*].RoleName'」を実行する。

![IAM](./IAM_23.png)  

(3)	信頼関係(AssumeRoleポリシー)を.jsonで定義する。

[`ポリシー ダウンロード`](./Trust.json)

(4)	IAM ロールの作成を行う。

「aws iam create-role `--role-name` ロール名 `--assume-role-policy-document` file:// <ファイルパス>」を実行する。
 
![IAM](./IAM_24.png)  

![IAM](./IAM_25.png)  
 
(5)	ポリシーのアタッチを行う。

「aws iam attach-role-policy `--policy-arn` arn:aws:iam::aws:policy/ポリシー名　`--role-name` ロール名」を実行する。

※カスタムポリシーの場合は

「aws iam attach-role-policy `--policy-arn` arn:<テナントID>:iam::aws:policy/ポリシー名　`--role-name` ロール名」を実行する。
 
![IAM](./IAM_26.png)  

![IAM](./IAM_27.png)  
 
(6)	アタッチされているマネージドポリシーの一覧を表示する。

「aws iam list-attached-role-policies `--role-name` ロール名」を実行する。

![IAM](./IAM_28.png)  
