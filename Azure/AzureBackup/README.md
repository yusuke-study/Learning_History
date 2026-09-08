# Azure Files の Azure Backup 手順

(1) Microsoft Azureで、「Recovery Services コンテナー」を検索してクリックする。

![Azurebackup](./Azurebackup_01.png)

(2) 「＋作成」をクリックする。

![Azurebackup](./Azurebackup_02.png)

(3) 「リソースグループ」を選択し、「資格情報コンテナ名(英数字であれば何でも良い)」を入力し、リージョンは「Japan East」のままで、「確認および作成」をクリックする。

![Azurebackup](./Azurebackup_03.png)

(4) デプロイが完了したら、「リソースに移動」をクリックする。

![Azurebackup](./Azurebackup_04.png)

(5) ストレージレプリケーションの種類は、後に変更できないので、必要であれば変更する。

![Azurebackup](./Azurebackup_05.png)

(6) 「バックアップ」タブの、「何をバックアップしますか？」で、 「Azure ファイル共有」を選択して、「バックアップ」をクリックする。

![Azurebackup](./Azurebackup_06.png)

(7) ストレージアカウントの「選択」をクリックして、右枠からストレージを選択して「OK」をクリックする。

その後、「バックアップの有効化」をクリックする。

![Azurebackup](./Azurebackup_07.png)

(8) 「バックアップポリシー」タブをクリックし、作成したポリシーをクリックする。

![Azurebackup](./Azurebackup_08.png)

(9) バックアップスケジュールを変更し、「更新」クリックする。

![Azurebackup](./Azurebackup_09.png)

(10) すぐにバックアップを行いたい場合は、ストレージアカウント＞ファイル共有＞バックアップ＞「今すくバックアップ」をクリックする。

![Azurebackup](./Azurebackup_10.png)

※ストレージアカウント＞ファイル共有＞バックアップ＞スナップショット から、バックアップされた日時が確認可能。

![Azurebackup](./Azurebackup_11.png)

「スナップショットの追加」をクリックし、「OK」をクリックすると、 Azure Backupの「今すくバックアップ」と同じように、 その時点のバックアップが作成される。

![Azurebackup](./Azurebackup_12.png)

(11) Azure Filesの中身をバックアップを取得した時間に戻したい時、

Azure Filesのネットワークドライブ上で右クリックし、「以前のバージョンの復元(V)」をクリックし、復元したい時間を選択し、「復元(R)」をクリックする。

![Azurebackup](./Azurebackup_13.png)
