# Angular
フロントエンドWebアプリケーションフレームワーク
[AngularCLI]
Angularアプリ開発のための公式コマンドラインツール
[コンポーネント]
ページを構成するUI部品、下記で構成
- コンポーネントクラス: コンポーネントの構成、HTMLテンプレートに渡すデータ、コンポーネントの振る舞いを定義
- HTMLテンプレート: レンダリングして、HTMLを作成
- スタイルシート: HTMLテンプレートの見栄え
- テストスクリプト: コンポーネントのテスト
[サービス]
サーバーとの通信部分などコンポーネント共通ロジックなど定義

# 環境構築(Linux)
[VM作成]
別途参照
[node「12」インストール]
curl -sL https://rpm.nodesource.com/setup_12.x | bash -
yum install nodejs
[Angular「9.1.7」インストール]
npm install -g @angular/cli@~9.1.7

# 基本コマンド
[プロジェクト作成(現在位置より作成される)]
ng new {プロジェクト名}
- ? Would you like to add Angular routing? (y/N): ルーティング機能を持たせるかどうか？基本「y」で進める
- ? Which stylesheet format would you like to use? (Use arrow keys): スタイルシートはどれを使うか？「CSS」で進める

# バックエンドとの通信
[HttpClientの取り込み]
app.module.ts
・import { HttpClientModule } from '@angular/common/http';
・@NgModule > importsに追加「HttpClientModule」
HttpClientを使いたいコンポーネント
・import { HttpClient } from '@angular/common/http';
・クラス > constructorに追加「private http: HttpClient」
[プロキシ設定ファイル作成]
cd {Angularプロジェクト直下}
「proxy.conf.json」作成
```
{
    "/api": {
        "target": "http://localhost:8080",
        "secure": false
    }
}
```
[リクエスト構文]
this.http.get('パス').subscribe(
    // 成功
    response => {
        成功時の処理
    },
    // 失敗
    error => {
        失敗時の処理
    }
);

[起動時にプロキシ設定]
ng serve --host 0.0.0.0 --proxy-config proxy.conf.json
