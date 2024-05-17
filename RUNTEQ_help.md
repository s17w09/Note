### [知ったかシリーズ（API編)](https://school.runteq.jp/v2/mypage/helps/articles/api_outline?gretel_word=%E8%A3%9C%E8%B6%B3%E3%83%BB%E4%BA%88%E5%82%99%E7%9F%A5%E8%AD%98)
- 「RubyでAPIを使用するとなると、専用のgemかFaraday というhttp client gemが使われることが多いです。」
- Faredayに関して
https://lostisland.github.io/faraday/#/
https://qiita.com/shimura_atsushi/items/73eca414e13887ea6fed
- http client gemとは
らんてくん：　RubyでHTTPリクエストを送るためのライブラリ。例えば、ウェブサイトからデータを取得したり、APIにデータを送信したりするのに使う。
APIを使用する際にHTTP Client Gemは必須ではなく、net/httpという標準ライブラリも使える。httpartyもHTTP Client Gemの一つ。

 - [The Ruby Toolbox](https://www.ruby-toolbox.com/categories/http_clients)で使用されているOSSがわかる


### [参考になるネットの記事と書籍について](https://school.runteq.jp/v2/mypage/helps/articles/summary_reference?gretel_word=%E8%A3%9C%E8%B6%B3%E3%83%BB%E4%BA%88%E5%82%99%E7%9F%A5%E8%AD%98)
- [Rails開発におけるwebサーバーとアプリケーションサーバーの違い](https://qiita.com/jnchito/items/3884f9a2ccc057f8f3a3)
- Webサーバー：
 > webサーバーはユーザーから送られてきた自サイトへのリクエストを受け取り、なんらかの処理を加えるプログラムです。そして、場合によってはあなたのRailsアプリケーションにリクエストを投げます。 NginxとApacheは最も有名なwebサーバーです。
- Applicationサーバー：
  >アプリケーションサーバーはあなたのRailsアプリケーションを動かしているものです。 アプリケーションサーバーはあなたのコードを読み込み、アプリケーションをメモリに保持します。アプリケーションサーバーはwebサーバーからリクエストを受け取ると、Railsアプリケーションにそのことを知らせます。アプリケーションがリクエストを処理すると、アプリケーションサーバーはそのレスポンスをwebサーバーに返します。（そのレスポンスは最終的にユーザーへ届きます。）
- Rack：
  >Rackは魔法です。Rackを使えばどのアプリケーションサーバーであってもあなたのRailsアプリケーションを動かすことができます。（Railsに限らず、SinatraやPadrinoであっても同じです）
RackはRailsのようなRuby製のwebフレームワークとアプリケーションサーバーの両方が話せる共通言語のようなものだと考えてください。両者が共通言語を理解できるので、RailsはUnicornと話せますし、UnicornはRailsと話せます。しかも、RailsもUnicornも相手のことを知っておく必要は全くありません。

- [早く知ってたら良かったrailsの技](https://qiita.com/k-shogo/items/5bbc23e1d0dd0ad3a8a2)
◉全般
- shallowオプション：new, createのアクションでは親リソースのIDがURLに含まれる。だけど、show,edit,update,destroyのアクションでは、/comments/:idのように、commentsだけのシンプルなURLパスになる https://www.notion.so/resources-shallow-2748642a86684dcf9794c3c4f93a6c5e?pvs=4
- ActiveModel:
  >DBには永続化しないんだけど、ActiveRecordと同じような使い勝手のモデルが欲しいなーと思うことがあります。
例えば検索用のフォームなどですね。
view で form_for 使いたいし、validate も同じように定義したいからです。
- delegateメソッド

◉MVC
