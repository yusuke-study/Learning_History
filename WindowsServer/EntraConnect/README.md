# Entra Connect

Entra Connectとは、Active Directoryのユーザーを、Entra IDに同期するシステムである。

## Entra Connect 設定

(1) Entra管理センターで「AzureADConnect.msi」をインストールする。

![EC](./EntraConnect_01.png)

(2) Entra Connect 管理するオンプレドメインサーバーで、ツールをインストールし、画面の手順に従って進む。

![EC](./EntraConnect_02.png)

(3) 基本的には「カスタマイズ」を選択する。

![EC](./EntraConnect_03.png)

![EC](./EntraConnect_04.png)

![EC](./EntraConnect_05.png)

(4) パスワードハッシュが基本的には無難。

![EC](./EntraConnect_06.png)

(5) Entra IDのアカウントでログインし、と紐づける

![EC](./EntraConnect_07.png)

![EC](./EntraConnect_08.png)

![EC](./EntraConnect_09.png)

(6) Active Directryの、Entra Connrct管理用のアカウントを「新しい AD アカウントを作成」を選択して入力する。

※Enterprise Admins,Domain Adminsに所属するアカウントを使用する必要有。

![EC](./EntraConnect_10.png)

![EC](./EntraConnect_11.png)

(7) UPNを選択する。

![EC](./EntraConnect_12.png)

(8) 同期するOUを選択する。

![EC](./EntraConnect_13.png)

![EC](./EntraConnect_14.png)

![EC](./EntraConnect_15.png)

(9) オプション機能を選択する。

![EC](./EntraConnect_16.png)

(10) インストールを開始する。

※同期を行わない場合は「ステージングモード」を選択する。

![EC](./EntraConnect_17.png)


## Entra Connect ユーザー＆グループ同期

(1) 同期対象のOUでユーザーとグループを作成する。

![EC](./EntraConnect_18.png)

(2) すぐに同期する場合は「Start-ADSyncSyncCycle -PolicyType Initial」を実行する。

![EC](./EntraConnect_19.png)

Synchronization Service Manager　での同期時間の確認も可能。

![EC](./EntraConnect_20.png)

(3) Entra ID で同期されたことを確認。

![EC](./EntraConnect_21.png)

![EC](./EntraConnect_22.png)

※補足コマンド

Active DirectoryからEntra IDへの同期スケジュールの確認、同期間隔の確認を行う際は「Get-ADSyncScheduler」を実行する。

※通常の同期は30分に1回である。

![EC](./EntraConnect_23.png)


