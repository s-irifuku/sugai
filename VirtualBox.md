# VirtualBox
ローカルPC上に仮想的なPCを作成し、別のOSをインストール・実行できるPC仮想化ソフト

# 検証環境構築手順
'''
[「VirtualBox」のインストール]
省略
[「CentOS-7-x86_64-DVD-2009.iso」のインストール]
省略
[VM作成]
「VirtualBox」で「新規」ボタン押下
・タイプ：Linux
・バージョン：Red Hat（64-bit）
・以降、デフォルトのまま進める
作成したらVM選択して「設定」ネットワークのアダプター2で
・ネットワークアダプターを有効化をチェック
・ホストオンリーアダプターを割り当て
[VM起動と初期設定]
「VirtualBox」で「起動」ボタン押下
起動ハードディスクを選択でDLしたisoファイルを選択
言語は日本語選択
「インストール先」で下記設定
　何も変更せず「完了」ボタン押下
「ネットワークとホスト名」で下記設定
　Ethernet(enp0s3)：オンにして「設定」で下記を行い保存
　　全般 > この接続が利用可能になったときは自動的に接続する：チェック
　　IPv6のセッティング > 方式：「無視する」に設定
　Ethernet(enp0s8)：オンにして「設定」で下記を行い保存
　　全般 > この接続が利用可能になったときは自動的に接続する：チェック
　　IPv6のセッティング > 方式：「無視する」に設定
「インストールの開始」押下してrootパスワード設定とユーザー作成
　rootパスワード：dev0330
　ユーザー作成：「irifuku:dev0330」

[Firewalld停止と自動起動無効化]
systemctl stop firewalld
systemctl disable firewalld

[SSHキー作成]
`cd /root`
`ssh-keygen -t rsa`
Generating public/private rsa key pair.
Enter file in which to save the key (/root/.ssh/id_rsa): {そのままEnter}
Enter passphrase (empty for no passphrase): {そのままEnter}
Enter same passphrase again: {そのままEnter}
「/root/.ssh/id_rsa」をローカル側にDLして、「C:\Users\User\.ssh」に移動
'''
