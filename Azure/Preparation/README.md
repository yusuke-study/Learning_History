
Azureを使用するための準備(CLIのログイン方法、サブスクリプションの付与、Role設定等)について記載する。

※前提条件：Windows PCに、Azure CLIがインストールされていること。


##	CLI 基本操作


(1)	Azureにログインする。

「az login」を実行する。

　実行すると、ブラウザでMicrosoft　Azureのログイン画面が表示されるので、ユーザー名とパスワードを入力する。

※コマンド実行の際に、下記内容でユーザー名とパスワードを指定することも可能である。

　az login --user <username> --password <password>
 

(2)	テナントIDやサブスクリプション情報を表示する。

「az account list -o table」を実行する。
 


(3)	ユーザーのオブジェクトIDを取得する。

「az ad user show --id <ユーザUPN> --query id --output tsv」を実行する。
 

(4)	ユーザーにサブスクリプション権限を付与する。

「az role assignment create --assignee <ユーザーのオブジェクトIDまたはUPN> --role "Contributor" --scope /subscriptions/<サブスクリプションID>」を実行する。
 
 
(5)	ロールの権限内容を表示する。

「az role definition list --name "<ロール名>"」を実行する。
 


(6)	カスタムロールのみ表示する。

「az role definition list --query "[?roleType=='CustomRole'].{Name:roleName, Type:roleType}" --output table」を実行する。
 
 

 
 
3.1.2	サブスクリプション付与(GUI)

Azure内のリソースを操作するうえでユーザーへのサブスクリプションの付与が必須である。

下記にGUIでサブスクリプションの付与方法について記載する。

(1)	Azure Portalにログインする。

(2)	「サブスクリプション」をクリックする。下記画面に表示されない場合は、検索窓で「サブスクリプション」等入力してサブスクリプションサービスのページに移動する。

  

 

(3)	サブスクリプション名をクリックする。
  

(4)	「アクセス制御(IAM)」をクリックする。
 

(5)	「ロールの割り当て」⇒「追加」をクリックする。
 

(6)	選択肢が表示されたら「ロール割り当ての追加」をクリックする。
 

(7)	特権管理者ロールタブの共同作成者を選択し、「次へ」をクリックする。

 

(8)	「＋メンバーを選択する」をクリックし、画面右に表示されるユーザー名をクリックする。

(9)	「選択したメンバー」に該当のユーザーが表示されたら「選択」をクリックする。

(10)名前の下にユーザーが表示されたら、「レビューと割り当て」を2回クリックする。


 

(11)「共同作成者」下に、先程追加したユーザーが表示されたら、アクセス権付与完了である。

  

今まで見られなかったサービスページが閲覧可能になる。

 　　　　　 
 
3.1.3	Role備考

Azureユーザー内で、アクセス権限(IAM)を編集できるのは、デフォルトでは所有者(Azureアカウントを作成した管理者)のみである。

他のユーザーでIAMの付与を行いたい場合、カスタムロールを作成し、ユーザーに権限を付与する必要がある。

下記に、GUIでカスタムロールを作成する手順を記載する。

※一般ユーザーの場合、下記のように編集ができない。
 

Admin権限のあるユーザーで、以下のような形式でJSONに記述する。
 


●ロールの管理を行う上で必要な権限は以下の通りである。

"Microsoft.Authorization/roleAssignments/write"

"Microsoft.Authorization/roleAssignments/delete"

"Microsoft.Authorization/roleAssignments/read"

 


●その他、指定したリソースの削除ロックを編集できる、削除できる権限は以下の通りである。
"Microsoft.Authorization/locks/write"
 "Microsoft.Authorization/locks/delete"
