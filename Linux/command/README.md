# Linux コマンド

※Linuxのコマンドについて、オペレーティングシステム（RHELやUbuntu）によって使用するコマンドやオプションが異なる場合があります。


(1) オペレーティングシステムの確認

hostnamectl

![command](./command_01.png)

(2) パーティションの確認

lsblk

![command](./command_02.png)

(3) ネットワーク設定の確認

/etc/netplan

![command](./command_03.png)

(4) hostsファイル情報の確認

/etc/hosts

![command](./command_04.png)

(5) ファイアウォールの確認

　# Ubuntuの場合

ufw status

![command](./command_05.png)

　# ファイアウォールの有効化

ufw enable

![command](./command_06.png)

　# ファイアウォールの追加

ufw allow　ポート等

ufw reload　#再読み込み

![command](./command_07.png)

　# RHEL等の場合

ステータス確認

systemctl status firewalld

![command](./command_12.png)

firewall-cmd --state

![command](./command_13.png)

許可されているサービス

firewall-cmd --list-all　　#その他コマンド有

![command](./command_14.png)

(6) 起動ランレベルの確認 

systemctl get-default

![command](./command_08.png)

　# ランレベルの変更

systemctl get-default　XXXXX

![command](./command_09.png)

(7) アカウント設定（共通）の確認

awk -F: '($3==0 || $3>=1000 && $3<60000) {
    user=$1; uid=$3; gid=$4; home=$6; shell=$7;
    cmd="id -nG " user;
    cmd | getline groups;
    close(cmd);
    printf "%s\t%s\t%s\t%s\t%s\t%s\n",
           user, uid, gid, shell, home, groups
}' /etc/passwd \
| { echo -e "USER\tUID\tGID\tSHELL\tHOME\tGROUPS"; cat; } \
| column -t -s $'\t'

![command](./command_10.png)

(8) パッケージ一覧(共通)の確認

　# Ubuntuの場合　 #バージョンを表示しない形式での出力

dpkg-query -W -f='${binary:Package}\n'　

![command](./command_11.png)

　# RHEL等の場合

dnf list installed

![command](./command_15.png)
