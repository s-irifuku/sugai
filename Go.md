# Go
関数型のコンパイル言語
'''
プラットフォーム(動作するのに必要な環境): ビルド時にOSに適合したネイティブコード生成することでマルチで動作(Windows,MacOS,Linux)
'''

# 環境構築(Linux)
[VM作成]
別途参照
[ログイン]
「root」でログインして進める。
[ワークスペース(開発フォルダ)作成]
mkdir -p /var/service/
[「Go本体」を配置するディレクトリに移動]
cd /var/service
[Go「1.18.3」ダウンロード]
curl -O https://dl.google.com/go/go1.18.3.linux-amd64.tar.gz
[解凍して「go本体」ディレクトリ作成]
tar xf go1.18.3.linux-amd64.tar.gz
[「PATH」にgo実行ファイルへのパス追加]
前提知識
・/root/.bash_profile: rootユーザーでbashログイン時に読み込まれる環境変数の設定ファイル
・PATH: 入力コマンドに対応する実行ファイルが格納されたフォルダー群、コロン区切りで複数フォルダーへのパスが登録されている。
「vi /root/.bash_profile」で下記のように編集
・「PATH=$PATH:$HOME/bin」→「PATH=$PATH:$HOME/bin:/var/service/go/bin」
[「/root/.bash_profile」再読み込み]
source /root/.bash_profile
[GOPATH設定]
GOPATH: ワークスペースのルートを表す変数、デフォルトはログインユーザーのホームディレクトリが指定されている。
「vi /root/.bash_profile」で下記を追記
'''
GOPATH=/var/service/go
export GOPATH
'''
[「/root/.bash_profile」再読み込み]
source /root/.bash_profile

# プロジェクト作成
「ワークスペース/go/src」直下にプロジェクトを作成する。
その中にmain.goや各パッケージフォルダを作成する。
