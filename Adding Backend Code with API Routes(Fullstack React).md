## Adding Backend Code with API Routes(Fullstack React).md
### What are API Routes? / Adding & Using API Routes / Working with Requests & Responses

#### What are API Routes?
- Rest API: REST アーキテクチャの制約に従って、RESTful Web サービスとの対話を可能にする アプリケーション・プログラミング・インタフェース。REST (Representational State Transfer) は、コンピュータ・サイエンティストの Roy Fielding によって作成された API の構築方法を定義する仕様であり、REST 用に設計された REST API (または RESTful API) は軽量で高速であるため、IoT (モノのインターネット)、モバイル・アプリケーション開発、サーバーレス・コンピューティングなどの先進的なコンテキストに最適。
  https://tech.012grp.co.jp/entry/rest_api_basics
  https://www.redhat.com/ja/topics/api/what-is-a-rest-api

- pages>api>~：　〜のファイル名は勝手に命名していいが、apiは固定。（apiフォルダはnext.jsに認識される特別なファイルのため）
- pages>api>feedback.jsの場合、URLはlocalhost:3000/api/feedbackになる
- apiフォルダ以外ではreactコンポーネント、export default使ええるが、api routes内ではreactコンポーネントは使えない
- だが、api routes内では下記のように書け、またserver side codeはなんでもかける
- リクエストを扱うのでhandler、handlerは2つのパラメーターを持つ、request objectとrespond object
```
function handler(req,res) {
  res.status(200).jason({ message: 'This works!'});
}

export default handler;
```
- これはJavaScriptの機能
