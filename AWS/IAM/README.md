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
「aws iam create-user --user-name <ユーザー名>」を実行する。
 
![IAM](./IAM_03.png)

![IAM](./IAM_04.png)

(4)	アクセスキーを作成する。

「aws iam create-access-key --user-name <ユーザー名>」を実行する。

![IAM](./IAM_05.png)

(5)	パスワードを設定する。

「aws iam create-login-profile --user-name <ユーザー名> --password '<パスワード>' --password-reset-required」を実行する。

![IAM](./IAM_06.png)

(6)	「パスワードのリセットが必要」設定の反映をする。

「aws iam attach-user-policy --user-name <ユーザー名> --policy-arn arn:aws:iam::aws:policy/IAMUserChangePassword」を実行する。

![IAM](./IAM_07.png)

## IAM グループ

IAMグループに関連するコマンドを記載する。

(1)	グループの一覧を表示する。

「aws iam list-groups」を実行する。

![IAM](./IAM_08.png)

(2)	グループ名だけ出力する。

「aws iam list-groups --query 'Groups[].GroupName'」を実行する。

![IAM](./IAM_09.png)

(3)	グループを作成する。

「aws iam create-group --group-name <グループ名>」を実行する。

 ![IAM](./IAM_10.png)

(4)	ユーザーをグループに追加する。

「aws iam add-user-to-group --user-name <ユーザー名> --group-name <グループ名>」を実行する。

 ![IAM](./IAM_11.png) 

(5)	ユーザーが所属しているグループを表示する。

「aws iam list-groups-for-user --user-name<ユーザー名>」を実行する。

 ![IAM](./IAM_12.png) 



## IAM ポリシー


IAMポリシーに関連するコマンドを記載する。

(1)	カスタムポリシーのみを一覧表示する。

「aws iam list-policies --scope Local」を実行する。

 ![IAM](./IAM_13.png) 

(2)	ユーザーにポリシーを付与する
「aws iam attach-user-policy --user-name <ユーザー名>  --policy-arn arn:aws:iam::aws:policy/<ポリシー名>」を実行する。
 
 ![IAM](./IAM_14.png) 
 
 ![IAM](./IAM_15.png) 

(3)	ユーザーにアタッチされているポリシーを表示する。
「aws iam list-attached-user-policies --user-name <ユーザー名>」を実行する。

![IAM](./IAM_16.png) 

(4)	グループにアタッチされているポリシーを表示する。
「aws iam list-attached-group-policies --group-name <グループ名> 」を実行する。
 
![IAM](./IAM_17.png) 

(5)	ポリシーを作成するための内容を定義する。

Jsonファイルを作成する。（例）

EC2のフルアクセス権限



(6)	ポリシーを作成する。
「aws iam create-policy --policy-name <ポリシー名> --policy-document file://<ファイルパス>」を実行する。
 
![IAM](./IAM_18.png) 

![IAM](./IAM_19.png) 


(7)	ポリシーの内容を表示する。
「aws iam get-policy-version --policy-arn <arn> --version-id v1」を実行する。

![IAM](./IAM_20.png) 

※JSON形式のポリシー一例は以下である。

![IAM](./IAM_21.png) 

IAMポリシーの基本構造（JSON）　一例  ※細かく設定する場合

{
    "Version": "2012-10-17",
    "Statement": [
        {
            "Effect": "Allow",
            "Action": [
                "iam:CreateRole",　　　　　#新しいIAMロールを作成
                "iam:DeleteRole",　　　　　#IAMロールを削除
                "iam:PutRolePolicy",　　　　　#インラインポリシーをロールに追加
                "iam:CreateInstanceProfile",　　　　　#ロールに付与されたインラインポリシーを削除
                "iam:DeleteRolePolicy",　　　　　#EC2にIAMロールをアタッチするためのプロファイルを作成
                "iam:AddRoleToInstanceProfile",　　　　　#インスタンスプロファイルを削除
                "iam:RemoveRoleFromInstanceProfile",　　　　　#インスタンスプロファイルにロールを追加
                "iam:DeleteInstanceProfile",　　　　　#インスタンスプロファイルからロールを削除
                "iam:PassRole",　　　　　#EC2などのサービスにロールを渡す
                "iam:ListRoles",　　　　　#IAMロールの一覧を取得
                "iam:GetRole",　　　　　#IAMロールの詳細情報を取得
                "iam:TagRole",　　　　　#IAMロールにタグを付与
                "ec2:DescribeInstanceStatus",　　　　　#インスタンスのステータスを取得
                "ec2:RunInstances",　　　　　#EC2インスタンスを起動
                "ec2:ModifyInstanceAttribute",　　　　　#インスタンスの属性を変更
                "ec2:CreateSecurityGroup",　　　　　#NSGを作成
                "ec2:DeleteSecurityGroup",　　　　　# NSGを削除
                "ec2:DescribeSecurityGroups",　　　　　#セキュリティグループの情報を取得
                "ec2:RevokeSecurityGroupEgress",　　　　　#アウトバウンドルールを削除
                "ec2:AuthorizeSecurityGroupEgress",　　　　　#アウトバウンド（送信）ルールを追加
                "ec2:AuthorizeSecurityGroupIngress",　　　　　#インバウンド（受信）ルールを追加
                "ec2:RevokeSecurityGroupIngress",　　　　　#インバウンドルールを削除
                "ec2:CreateNetworkInterface",　　　　　#ENI（Elastic Network Interface）を作成
                "ec2:DescribeNetworkInterfaces",　　　　　#ENIの情報を取得
                "ec2:DeleteNetworkInterface",　　　　　#ENIを削除
                "ec2:ModifyNetworkInterfaceAttribute",　　　　　#ENIの属性を変更
                "ec2:DescribeSubnets",　　　　　#サブネットの情報を取得
                "ec2:DescribeVpcs",　　　　　#VPCの情報を取得
                "ec2:DescribeDhcpOptions",　　　　　# DHCPオプションセットの情報を取得
                "ec2:DescribeKeyPairs",　　　　　#EC2インスタンス用のSSHキーペア一覧を取得
                "ec2:DescribeRegions",　　　　　#利用可能なリージョン一覧を取得
                "ec2:DescribeInstances",　　　　　#EC2インスタンスの情報を取得
                "ec2:CreateTags",　　　　　# EC2リソースにタグを付与
                "ec2:DescribeImages",　　　　　# AMI（Amazon Machine Image）の情報を取得
                "ec2:DescribeAvailabilityZones",　　　　　#利用可能なアベイラビリティゾーンを取得
                "ec2:DescribeLaunchTemplates",　　　　　#起動テンプレートの情報を取得
                "ec2:CreateLaunchTemplate",　　　　　# EC2起動テンプレートを作成
                "ec2:AssociateIamInstanceProfile",　　　　　#EC2にIAMプロファイルを関連付け
                "ec2:DescribeIamInstanceProfileAssociations",　#EC2からIAMプロファイルを解除
                "ec2:DisassociateIamInstanceProfile",　　　　　#インスタンスプロファイルの関連付け状況を取得
                "cloudformation:CreateStack",　　　　　#CloudFormationスタックを新規作成
                "cloudformation:DeleteStack",　　　　　#スタックを削除
                "cloudformation:DescribeStacks",　　　　　#スタックの詳細情報を取得
                "cloudformation:DescribeStackEvents",　　　　　#スタックのイベント履歴を取得
                "cloudformation:ValidateTemplate",　　　　　#CloudFormationテンプレートの構文チェック
                "cloudformation:ListStacks"　　　　　#スタックの一覧を取得
                "kms:ListAliases",　　　　　#KMSキーのエイリアス一覧を取得
            ],
            "Resource": "*"　　　　　　　　　　#すべて対象とする
        },
        {
            "Effect": "Allow",　　　　　#このポリシーは許可（Allow）を与える
            "Action": [
                "ec2:TerminateInstances"　　　　　#EC2インスタンスの削除（Terminate）操作を許可
            ],
            "Condition": {
                "StringLike": {　　　　　　　　　　　　　　#条件付きで許可
                    "ec2:ResourceTag/OCCMInstance": "*"　　　　#EC2インスタンスに OCCMInstance というタグが付いていれば、どんな値でも許可対象にする
                }
            },
            "Resource": [
                "arn:aws:ec2:*:*:instance/*"　　　　　#すべてのリージョン・アカウントのEC2インスタンスが対象
            ]
        }
    ]



## IAM ロール


## AWS Organizations
