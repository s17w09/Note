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
#### [Rails開発におけるwebサーバーとアプリケーションサーバーの違い](https://qiita.com/jnchito/items/3884f9a2ccc057f8f3a3)
- Webサーバー：
 > webサーバーはユーザーから送られてきた自サイトへのリクエストを受け取り、なんらかの処理を加えるプログラムです。そして、場合によってはあなたのRailsアプリケーションにリクエストを投げます。 NginxとApacheは最も有名なwebサーバーです。
- Applicationサーバー：
  >アプリケーションサーバーはあなたのRailsアプリケーションを動かしているものです。 アプリケーションサーバーはあなたのコードを読み込み、アプリケーションをメモリに保持します。アプリケーションサーバーはwebサーバーからリクエストを受け取ると、Railsアプリケーションにそのことを知らせます。アプリケーションがリクエストを処理すると、アプリケーションサーバーはそのレスポンスをwebサーバーに返します。（そのレスポンスは最終的にユーザーへ届きます。）
- Rack：
  >Rackは魔法です。Rackを使えばどのアプリケーションサーバーであってもあなたのRailsアプリケーションを動かすことができます。（Railsに限らず、SinatraやPadrinoであっても同じです）
RackはRailsのようなRuby製のwebフレームワークとアプリケーションサーバーの両方が話せる共通言語のようなものだと考えてください。両者が共通言語を理解できるので、RailsはUnicornと話せますし、UnicornはRailsと話せます。しかも、RailsもUnicornも相手のことを知っておく必要は全くありません。

#### [早く知ってたら良かったrailsの技](https://qiita.com/k-shogo/items/5bbc23e1d0dd0ad3a8a2)
◉全般
- shallowオプション：new, createのアクションでは親リソースのIDがURLに含まれる。だけど、show,edit,update,destroyのアクションでは、/comments/:idのように、commentsだけのシンプルなURLパスになる https://www.notion.so/resources-shallow-2748642a86684dcf9794c3c4f93a6c5e?pvs=4
- ActiveModel:
  >DBには永続化しないんだけど、ActiveRecordと同じような使い勝手のモデルが欲しいなーと思うことがあります。
例えば検索用のフォームなどですね。
view で form_for 使いたいし、validate も同じように定義したいからです。
- delegateメソッド

◉MVC
#### [中規模Web開発のためのMVC分割とレイヤアーキテクチャ](https://qiita.com/yuku_t/items/961194a5443b618a4cac)
>レイヤアーキテクチャというのはアプリケーションを責務に応じたいくつかの層としてとらえる設計手法のことです。
>このとき上の層が下の層を一方的に利用するようにすることで、オブジェクト間の結合を疎に保ちます
[![Image from Gyazo](https://i.gyazo.com/17a3b357d6354e4e468e526a71cd6f01.png)](https://gyazo.com/17a3b357d6354e4e468e526a71cd6f01)

#### [Webアプリケーション開発者から見た、MVCとMVP、そしてMVVMの違い](https://qiita.com/shinkuFencer/items/f2651073fb71416b6cd7)
>Railsで語られるMVCと他で語られるMVCのニュアンスが若干違うので
そこを基点にMVCの違い、そしてMVP、MVVMとは何なのかをまとめてみました。
- RailsのMVCは理解できたが、他言語のMVC, MVP, MVVMの理解はできていない。だが、Rails以外の時は、知っている単語でもいいが違うということは改めて理解できた。

◉ActiveRecord
#### [【Rails】 マイグレーションファイルを徹底解説！](https://pikawaka.com/rails/migration)
> railsでデータベースに対して何らかの変更を行いたい場合、全てマイグレーションファイルというファイルを作成・編集して読み込ませることによりテーブルを作成したり、カラムを追加したりします。
- NoFileと表示されたら：[これみる](https://pikawaka.com/rails/migration#%E9%96%93%E9%81%95%E3%81%A3%E3%81%A6%E5%89%8A%E9%99%A4%E3%81%97%E3%81%A6%E3%81%97%E3%81%BE%E3%81%A3%E3%81%9F%E3%82%89)
- カラムの型：bigint（かなり大きな整数型を保存したい時）、boolean（true又はfalseを保存したい時）

#### [Rails 5から導入されたmigration versioingについて](https://y-yagi.tumblr.com/post/137935511450/rails-5%E3%81%8B%E3%82%89%E5%B0%8E%E5%85%A5%E3%81%95%E3%82%8C%E3%81%9Fmigration-versioing%E3%81%AB%E3%81%A4%E3%81%84%E3%81%A6)
マイグレーションファイルの一番上に生成される、```class CreateInvitations < ActiveRecord::Migration[5.2]```の[5.2]は、Railsのバージョン。
今が、v7.1だけど、マイグレーションファイルに古いバージョンで記載ある場合は、その古いバージョンの挙動をそのまま保持できるので、互換性を維持することができる。

#### [Railsバリデーションまとめ](https://qiita.com/h1kita/items/772b81a1cc066e67930e)
- 「バリデーションがトリガされる」：　データのチェック（バリデーション）が行われるきっかけが発生することを意味する

- numericality：　属性に数値のみが使われていることをバリデーションします。デフォルトでは、整数値または浮動小数点数値にマッチする。https://railsguides.jp/active_record_validations.html#numericality
- validates_associated：　常に有効でなければならない関連付けがモデルにある場合は、このヘルパーを使う
  https://railsguides.jp/active_record_validations.html#validates-associated
- :ifや:unlessでProcを使う：　Procオブジェクトを使うと、個別のメソッドを指定する代わりに、その場で条件を書けるようになります。ワンライナーに収まる条件を使いたい場合に最適です。https://railsguides.jp/active_record_validations.html#if%E3%82%84-unless%E3%81%A7proc%E3%82%92%E4%BD%BF%E3%81%86


#### [Rails tips: 知らないと損する4つのバリデーションレベル（翻訳）](https://techracho.bpsinc.jp/hachi8833/2021_12_02/55771)
- コントローラーレベルでのバリデーション：　Form objectパターン

- ロボらんてくん　FormObject解説：
>OK、RailsのForm Objectについて簡単に説明するゾ！

###### Form Objectとは？
Form Objectは、複雑なフォームを扱うためのデザインパターンなんダ。通常はActiveRecordモデルのバリデーションやロジックをフォーム専用のクラスに分離することで、コードを整理しやすくする目的があるんダナ。

###### いつ使うのか？
複数のモデルを一つのフォームで扱いたいとき
フォームに特定のバリデーションやロジックを追加したいとき
フォームの再利用性を高めたいとき
###### 基本的な使い方
1,  Form Objectクラスを作成

通常のクラスを作成して、ActiveModel::Modelをincludeする。
```
class UserForm
  include ActiveModel::Model

  attr_accessor :name, :email

  validates :name, presence: true
  validates :email, presence: true, format: { with: URI::MailTo::EMAIL_REGEXP }

  def save
    return false unless valid?
    # 保存ロジックをここに書く
  end
end
```
2,  フォームで使用

コントローラーでForm Objectを使ってデータを受け取り、バリデーションや保存を行う。
```
class UsersController < ApplicationController
  def new
    @user_form = UserForm.new
  end

  def create
    @user_form = UserForm.new(user_form_params)
    if @user_form.save
      redirect_to success_path
    else
      render :new
    end
  end

  private

  def user_form_params
    params.require(:user_form).permit(:name, :email)
  end
end
```

###### メリット
コードの整理: モデルの肥大化を防ぎ、フォームに特化したロジックを専用のクラスに分けることができる。
テストが容易: フォームのバリデーションやロジックを個別にテストしやすくなる。
これがRailsのForm Objectの基本的な使い方なんダナ。

#### [【初心者向け】丁寧すぎるRails『アソシエーション』チュートリアル【幾ら何でも】【完璧にわかる】](https://qiita.com/kazukimatsumoto/items/14bdff681ec5ddac26d1)
- Rails基礎内容＋followfollowerの関係がわかる、わかりやすい記事

#### [railsのnewとbuildの違い](https://qiita.com/ryosuke-endo/items/6bae532b4f678fdcf87d)
- 結論は同じ役割を持つ

◉コントローラー
#### [RailsでAction Controllerについて学んでみた](https://thinkit.co.jp/story/2015/09/03/6389)
- [Model.find(params[:id]) を丁寧に調べた（Rails入門）](https://qiita.com/ryosuketter/items/44005785f47136a83ae1)
- [Railsで出てくるparams[:id]ってなんだ？paramsについて深く理解してみる](https://qiita.com/mokio/items/05cd9f12aae9e2395676)

- ロボらんてくん paramsの使い方まとめ
```
find(params[:id])
使い方: findメソッドは特定のIDに対応する既存のレコードをデータベースから取得ために使う。
例: current_user.boards.find(params[:id])は、現在のユーザーの中から特定のIDのボードを探す。
build(board_params)
使い方: buildメソッドは新しいレコード（＝行）を作成するために使う。引数には新しいレコードの属性を含むハッシュ（この場合はboard_params）を渡す。
例: current_user.boards.build(board_params)は、現在のユーザーに関連する新しいボードを作成する。
まとめ
find(params[:id]): 既存のレコードをIDで検索。
build(board_params): 新しいレコードを属性ハッシュで作成。
だから、params[:id]とboard_paramsの書き方が異なるのは、findとbuildの使い方が異なるからなんダナ
```
