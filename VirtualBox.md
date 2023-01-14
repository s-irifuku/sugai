# VirtualBox
ローカルPC上に仮想的なPCを作成し、別のOSをインストール・実行できるPC仮想化ソフト
'''
[NAT]
「VirtualBoxで作成したゲストOS」から「外部ネットワーク(インターネット含む)」に向けた通信が可能になる仮想ネットワークアダプター
ネットワークインターフェース「enp0s3」で動作している。DHCPでIPアドレスが割り当てられている。

[ホストオンリーアダプター]
「ホストOS」から「VirtualBoxで作成したゲストOS」に通信が可能になる仮想ネットワークアダプター
ネットワークインターフェース「enp0s8」で動作している。
'''

# ホストオンリーアダプター作成手順
1. 「ファイル > ホストネットワークマネージャー」で「作成」押下
2. アダプター設定
    アダプターを手動で設定：チェック
    IPv4アドレス：192.168.56.1
    IPv4ネットマスク：255.255.255.0
3. DHCPサーバー設定
    サーバーを有効化：チェック
    サーバーアドレス：192.168.56.100
    サーバーマスク：255.255.255.0
    アドレス下限：192.168.56.101
    アドレス上限：192.168.56.254

# 検証環境構築手順
1. VirtualBoxインストール
    省略
2. ISOファイル「CentOS-7-x86_64-DVD-2009.iso」インストール
    省略
3. VM作成
    「VirtualBox」で「新規」ボタン押下
    タイプ：Linux
    バージョン：Red Hat（64-bit）
    以降、デフォルトのまま進める
4. ネットワーク設定にホストオンリーアダプター追加
    ネットワークアダプターを有効化：チェック
    ホストオンリーアダプターを割り当て
5. VM起動と初期設定
    1. 「VirtualBox」で「起動」ボタン押下
    2. 起動ハードディスクを選択でDLしたisoファイルを選択
    3. 言語は日本語選択
    4. 「インストール先」で下記設定
        何も変更せず「完了」ボタン押下
    5. 「ネットワークとホスト名」で下記設定
        Ethernet(enp0s3)：オンにして「設定」で下記を行い保存
            全般 > この接続が利用可能になったときは自動的に接続する：チェック
            IPv6のセッティング > 方式：「無視する」に設定
        Ethernet(enp0s8)：オンにして「設定」で下記を行い保存
            全般 > この接続が利用可能になったときは自動的に接続する：チェック
            IPv6のセッティング > 方式：「無視する」に設定
    6. 「インストールの開始」押下してrootパスワード設定とユーザー作成
　          rootパスワード：dev1234
            ユーザー作成：「irifuku:dev1234」
6. Firewalld停止と自動起動無効化
    systemctl stop firewalld
    systemctl disable firewalld
7. SSHキー作成
    cd /root
    ssh-keygen -t rsa
    Generating public/private rsa key pair.
    Enter file in which to save the key (/root/.ssh/id_rsa): {そのままEnter}
    Enter passphrase (empty for no passphrase): {そのままEnter}
    Enter same passphrase again: {そのままEnter}
    「/root/.ssh/id_rsa」をローカル側にDLして、「C:\Users\User\.ssh」に移動
