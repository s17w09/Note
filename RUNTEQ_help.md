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
- [中規模Web開発のためのMVC分割とレイヤアーキテクチャ](https://qiita.com/yuku_t/items/961194a5443b618a4cac)
>レイヤアーキテクチャというのはアプリケーションを責務に応じたいくつかの層としてとらえる設計手法のことです。
>このとき上の層が下の層を一方的に利用するようにすることで、オブジェクト間の結合を疎に保ちます
[![Image from Gyazo](https://i.gyazo.com/17a3b357d6354e4e468e526a71cd6f01.png)](https://gyazo.com/17a3b357d6354e4e468e526a71cd6f01)

- [Webアプリケーション開発者から見た、MVCとMVP、そしてMVVMの違い](https://qiita.com/shinkuFencer/items/f2651073fb71416b6cd7)
>Railsで語られるMVCと他で語られるMVCのニュアンスが若干違うので
そこを基点にMVCの違い、そしてMVP、MVVMとは何なのかをまとめてみました。
- RailsのMVCは理解できたが、他言語のMVC, MVP, MVVMの理解はできていない。だが、Rails以外の時は、知っている単語でもいいが違うということは改めて理解できた。

◉ActiveRecord
- [【Rails】 マイグレーションファイルを徹底解説！](https://pikawaka.com/rails/migration)
> railsでデータベースに対して何らかの変更を行いたい場合、全てマイグレーションファイルというファイルを作成・編集して読み込ませることによりテーブルを作成したり、カラムを追加したりします。
- NoFileと表示されたら：[これみる](https://pikawaka.com/rails/migration#%E9%96%93%E9%81%95%E3%81%A3%E3%81%A6%E5%89%8A%E9%99%A4%E3%81%97%E3%81%A6%E3%81%97%E3%81%BE%E3%81%A3%E3%81%9F%E3%82%89)
- カラムの型：bigint（かなり大きな整数型を保存したい時）、boolean（true又はfalseを保存したい時）

- [Rails 5から導入されたmigration versioingについて
](https://y-yagi.tumblr.com/post/137935511450/rails-5%E3%81%8B%E3%82%89%E5%B0%8E%E5%85%A5%E3%81%95%E3%82%8C%E3%81%9Fmigration-versioing%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)
マイグレーションファイルの一番上に生成される、```class CreateInvitations < ActiveRecord::Migration[5.2]```の[5.2]は、Railsのバージョン。
今が、v7.1だけど、マイグレーションファイルに古いバージョンで記載ある場合は、その古いバージョンの挙動をそのまま保持できるので、互換性を維持することができる。
