### Ruby入門
#### 1章 Rubyを動かす環境設定
- docker compose run --rm app bash：　docker-compose.ymlに定義されたappサービスの新しいコンテナを起動し、その中でbashシェルを実行し、終了後にコンテナを自動的に削除するという意味ダナ。
- 「--rm」：コンテナが停止した後、自動的に削除するオプションダナ。= コンテナがexited状態になったあと、自動的にコンテナを削除してくれる
- irb（Interactive Ruby）は、対話形式でRubyコードを実行できるツールです。実験的にコードを試すのに便利です。
  
```
putsメソッドは、引数を文字列として出力し、最後に改行を追加します。返り値はnilです。
printメソッドは、引数を文字列として出力しますが、改行は追加しません。返り値はnilです。
pメソッドは、引数をそのまま出力します。返り値は引数そのものです。
通常はputsメソッドを使用することが多いですが、配列やハッシュなどのオブジェクトを出力する場合は、pメソッドを使用するとオブジェクトの中身を確認しやすくなります。
```

[![Image from Gyazo](https://i.gyazo.com/3146e1181414ba6bcd86b1048c487e8c.png)](https://gyazo.com/3146e1181414ba6bcd86b1048c487e8c)

#### 2章 Rubyを使った簡単なプログラムの作成
[![Image from Gyazo](https://i.gyazo.com/98fe3e27a3bc4ec26424e07860a85bae.png)](https://gyazo.com/98fe3e27a3bc4ec26424e07860a85bae)
- シングルクオート(' ')とダブルクオート(" ")はRubyで文字列を囲むために使用されます。シングルクオートはその中の内容をそのまま出力し、ダブルクオートは式展開などを扱うことができます。
- ※シングルクオートで囲まれた文字列の中では、式展開は行われません。

```
name = "Ruby"
puts 'シングルクオート: Hello, #{name}' # 出力: シングルクオート: Hello, #{name}
puts "ダブルクオート: Hello, #{name}" # 出力: ダブルクオート: Hello, Ruby
```

#### 変数展開
> 文字列の中で変数を展開する方法を式展開といいます。Rubyの式展開は、ダブルクオートで囲まれた文字列の中で、#{}を使って変数や式を展開します。この方法を使うことで、文字列の中に変数の値を埋め込むことができます。※シングルクオートで囲まれた文字列の中では、式展開は行われません。

#### 定数
> 定数は、値が変わらない（または変更されることが少ない）データを保存するために使用します。Rubyでは、定数は大文字で始まります。通常、一度定義された定数の値は変更しないことが推奨されています。
再代入を行うと警告が表示されます。定数を使用することで、プログラムの可読性や保守性が向上します。例えば、円周率や税率などの値を定数として定義しておくと、これらの値を一元管理でき、誤って変更されるリスクを減らせます。


#### 3章 プログラムを制御する
**比較演算子**
[![Image from Gyazo](https://i.gyazo.com/caabd8c5eafa79b88ff5eeef85424af7.png)](https://gyazo.com/caabd8c5eafa79b88ff5eeef85424af7)

**論理演算子**
[![Image from Gyazo](https://i.gyazo.com/cf9f68182b967926cc3ca63768e47646.png)](https://gyazo.com/cf9f68182b967926cc3ca63768e47646)
- &&演算子：　左右の値が両方ともtrueの場合に、trueを返す
- 捉え方として左辺がtrueの場合は、右辺を返すことになる、というのと同義
- ||演算子：　左右の値のどちらかがtrueの場合に、trueを返す
- 捉え方として、左辺がfalseの場合は、右辺を返すことになる、というのと同義

#### 4章 配列の基本
- Rubyの配列は、異なるデータ型の要素を混在させることも可能

```
mixed_array = [1, "two", 3.0, [4, 5], {six: 6}]
```

- Rubyでは、負のインデックスを使って配列の最後から要素にアクセスすることもできる
```
fruits = ["apple", "banana", "cherry", "date", "elderberry"]
puts fruits[-1]
puts fruits[-2]
puts fruits[-3]

=> elderberry, date, cherryの順で出力される
```

- <<メソッドを使って要素を追加する = pushと同じ動きをする（＝配列の末尾に要素を追加する）
```
fruits = ["apple", "banana"]
fruits << "cherry"
p fruits

=> ["apple", "banana", "cherry"]

```

- unshiftメソッド：　配列の先頭に要素を追加する
- insertメソッド：　指定したインデックスに要素を追加する

```
fruits = ["apple", "banana"]
fruits.insert(1, "cherry")
p fruits # ["apple", "cherry", "banana"]
```

[![Image from Gyazo](https://i.gyazo.com/d25ac0658e8e010bb38cd8e602c44dff.png)](https://gyazo.com/d25ac0658e8e010bb38cd8e602c44dff)

- deleteメソッドを使うと、指定した要素を削除する
```
fruits = ["apple", "banana", "cherry", "banana"]
fruits.delete("banana")
p fruits # ["apple", "cherry"]
```

- delete_atメソッド：　指定したインデックスの要素を削除する
```
fruits = ["apple", "banana", "cherry"]
fruits.delete_at(1)
p fruits # ["apple", "cherry"]
```

[![Image from Gyazo](https://i.gyazo.com/b814c5fef2581cffa670e43f9d830d49.png)](https://gyazo.com/b814c5fef2581cffa670e43f9d830d49)

- each_with_indexメソッド：　何回目の繰り返しかを示すインデックスを取得する。
```
fruits = ["apple", "banana", "cherry"]

fruits.each_with_index do |fruit, index|
  puts "#{index}: #{fruit}"
end

=> 0: apple
1: banana
2: cherry
```

- indexを使って要素を変更する
```
fruits = ["apple", "banana", "cherry"]
fruits[1] = "avocado"
p fruits

=> ["apple", "avocado", "cherry"]
```

#### 5章 配列の基本
- uniqメソッド：　配列の要素から重複を取り除いた新しい配列を作成することができる。その際、元の配列は変更されない。
[![Image from Gyazo](https://i.gyazo.com/7ee5ac87d05b803ac7ed8ee6a3d0dfe1.png)](https://gyazo.com/7ee5ac87d05b803ac7ed8ee6a3d0dfe1)

uniqメソッドを使用しないで解いた場合の回答：
> numbersの要素を一つずつ取り出し、unique_numbersに取り出した要素が含まれていないかを確認しています。unique_numbersにnumberの値が含まれていない場合のみ、<<メソッドを使用してunique_numbersにnumberを追加しています。
```
numbers = [1, 2, 2, 3, 4, 4, 5, 5, 5]
unique_numbers = []
numbers.each do |number|
  if !unique_numbers.include?(number)
    unique_numbers << number
  end
end
p numbers
p unique_numbers
```
- sortメソッド：　配列の要素を昇順に並び替えることができる。元の配列は変更されず、新しい配列が作成される。
- length, sizeメソッド：要素数を取得するメソッド。

#### 6章 Hashの基本
- シンボルを使用すると、メモリの使用量が少なくなるため、シンボルを使用することが推奨されています。
- 外部のサービスと連携する場合など、キーが文字列で返ってくる場合は、文字列でキーを指定して値を取得します。

```
hash1 = { name: "Alice", age: 30 }
hash2 = { city: "Wonderland" }
hash3 = { name: "Bob", age: 20 }

merged_hash_with_conflict = hash1.merge(hash3)
puts merged_hash_with_conflict
```
=> {:name=>"Bob", :age=>20}と表示される
- hash1とhash3は、nameとageのキーが重複しているため、mergeメソッドを使用すると、mergeメソッドの引数で指定したhash3の値のBob, 20が優先されます。


#### 7章 メソッドについて
- メソッド：　プログラムの特定の機能を実行するためのコードの塊
- メソッドを使うことで、同じ処理を繰り返し記述する手間を省くことができます。コードの重複を避け、プログラム全体の可読性とメンテナンス性が向上します。

- デフォルト引数を使うことで、引数が渡されなかった場合に使用されるデフォルトの値を指定できます。

- シンプルな引数の場合は、括弧を省略して半角スペース区切りでメソッド名と引数を記述して呼び出すこともできます。
```
def greet(name)
  puts "Hello, #{name}!"
end

greet("Alice")
greet "Bob"
```

- 可変長引数: 任意の数の引数をメソッドに渡すことができます。可変長引数はアスタリスク（*）を使って定義し、渡された引数は配列として扱われます。

```
def greet(*names)
  names.each do |name|
    puts "Hello, #{name}!"
  end
end

greet("Alice", "Bob", "Carol")
```
=> Hello, Alice!
Hello, Bob!
Hello, Carol!と表示される

- ※変数は変数名の最初の一文字によって、ローカル変数、インスタンス変数、クラス変数、グローバル変数などの区別がされます。
- 変数名の最初の文字が小文字かアンダーバーから始まる変数はローカル変数と呼ばれます。
```
def greet
  message = "Hello, Ruby!"
  puts message
end

greet
puts message
```
=> Hello, Ruby!
chapter7/scope.rb:6:in `<main>': undefined local variable or method `message' for main:Object (NameError)


#### 8章　クラスについて
- Rubyで扱われる全てのデータはオブジェクトとして扱われます。
- オブジェクトはクラスに属しており、クラスという設計図に基づいて作成されたもののことです。
- 例えば、"あ"という文字列はStringクラスから生成されたオブジェクトであり、1という数値はIntegerクラスから生成されたオブジェクトです。
- プログラミング言語によっては、数やそれ以外のプリミティブな型はオブジェクトとしては扱われませんが、Rubyでは全てのデータがオブジェクトとして扱われるという特徴があります。

- クラスには、オブジェクトが持つべきデータや振る舞いを定義するためのメソッドが含まれます。
- クラスはClassキーワードを使って定義します。Classの後にクラス名を記述し、endで囲うことでクラスを定義します。
- Person.newは、Personクラスのインスタンスを生成するためのコードです。
#<Person:0x00007f1338d44520>のPersonはクラスの名を表し、0x00007f1338d44520はそのインスタンスのオブジェクトIDを示しています。
オブジェクトIDは、Rubyがオブジェクトを識別するための一意のIDで、実行するたびに異なる値が生成されます。

- 通常の変数はメソッドの中でのみ使用できるといったルールがありますが、インスタンス変数はクラスのインスタンスの中のメソッドであればどこからでも値を参照することができます。

- インスタンスメソッドは、クラスのインスタンスによって呼び出されるメソッドです。インスタンス変数を操作したり、インスタンスごとに異なる動作を行うために使用されます。
```
class Person
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def introduce_text
    "私の名前は#{name}です。#{age}才です"
  end
end

tarou = Person.new("太郎", "30")
puts tarou.introduce_text

hanako = Person.new("花子", "25")
puts hanako.introduce_text

=> 私の名前は太郎です。30才です
私の名前は花子です。25才です
```

- クラスメソッドは、クラス自体に関連付けられたメソッドです。インスタンスからは呼び出すことができず、クラス自体から呼び出すことができます。
- クラスメソッドを定義するときは、メソッド名の前にself.を付けます。
```
class Person
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def introduce_text
    "私の名前は#{name}です。#{age}才です"
  end

  def self.adulthood_age_text
    "成人年齢は18才です"
  end
end

puts Person.adulthood_age_text

=> 成人年齢は18才です
```

- privateメソッドは、そのクラスの内部からのみ呼び出すことができるメソッドです。
```
class Person
  attr_accessor :name, :age

  def initialize(name, age)
    @name = name
    @age = age
  end

  def introduce_text
    "私の名前は#{name}です。#{age}才です。私の秘密は#{secret}です。"
  end
  
  private

  def secret
    '内緒'
  end
end
  
person = Person.new("太郎", 30)
puts person.introduce_text
=> 私の名前は太郎です。30才です。私の秘密は内緒です。
```

#### 9章 モジュールについて
- Rubyのモジュールは、共通のメソッドや定数をまとめてグループ化する仕組みです。
- クラスとは異なり、インスタンスを生成することはできませんが、他のクラスやモジュールに対して機能を追加することができます。

- includeは、モジュールのメソッドをクラスのインスタンスメソッドとして取り込むためのキーワードです。
- extendは、モジュールのメソッドをクラスのクラスメソッドとして取り込むためのキーワードです。
```
class Person
  self.hello
    "Hello!"
  end
end
```

#### 10章 Rubyを使った複雑な操作(1)
- Webアプリケーション = クライアント（ブラウザやモバイルアプリなど）とサーバーが通信すること

- リクエスト：　クライアントがサーバーに対して情報を要求すること
- レスポンス：　　サーバーがその要求に対して情報を返すこと

- HTTPリクエストは、主に以下の部分から構成されます。
```
HTTPメソッド: リクエストの種類を示します（例: GET, POST, PUT, DELETE）。
URL: アクセスしたい場所を示します。
HTTPヘッダー: リクエストに関する追加情報（例: クライアントの情報、認証情報）。
HTTPボディ: リクエストに含めるデータ（POSTリクエストなどで使用）。
```

- HTTPレスポンスは、主に以下の部分から構成されます。
```
ステータスライン: リクエストの結果を示します（例: 200 OK, 404 Not Found）。
HTTPヘッダー: レスポンスに関する追加情報（例: コンテンツの種類、長さ）。
HTTPボディ: リクエストに対する実際のデータ（HTML、JSON、画像など）。
```

- JSON（ジェイソン）は、データ交換フォーマットの一つで、人間にも機械にも読みやすいテキスト形式です。
- 主にAPIなどのWebアプリケーションにおけるデータの送受信に使われます。JSONは、シンプルな構造と軽量であることから広く利用されています

#### 11章 Rubyを使った複雑な操作(2)
正規表現
- scanメソッドを使うと、文字列内の正規表現パターンに一致する部分文字列を配列で取得することができます。
```
pattern = /Ruby/

puts "Ruby".scan(pattern)
puts "Ruby Ruby".scan(pattern)

=> ["Ruby"]
["Ruby", "Ruby"]
```

- gsubメソッドを使うと、文字列内の正規表現パターンに一致する部分文字列を置換することができます。
```
p 'abcdefg'.gsub(/def/, '!!')          # => "abc!!g"
p 'abcabc'.gsub(/b/, '<<\&>>')         # => "a<<b>>ca<<b>>c"
p 'xxbbxbb'.gsub(/x+(b+)/, 'X<<\1>>')  # => "X<<bb>>X<<bb>>"
p '2.5'.gsub('.', ',') # => "2,5"
```
***
### データベース入門
#### 1章 データベースとは何か
- データベースとは「データの集まり」を指す概念であり、そのデータベースを効率的に管理・操作するためのシステムがDBMS（Database Management System：データベース管理システム）
- DBMSは、データベースを効率的に管理・操作するためのソフトウェアです。データベースそのものは単なるデータの集まりですが、DBMSはこのデータに対して様々な操作（追加、更新、削除、検索など）を可能にします。

#### 2章 リレーショナルデータベース
- 多くの種類のデータベースが使用されています。
- 主なものには、階層データモデル、ネットワークデータモデル、リレーショナルデータモデルがあります。
- 階層データモデルはデータをツリー構造で管理
- ネットワークデータモデルはより複雑なネットワーク構造を使用します。
- リレーショナルデータモデルは、データを表形式で管理します。各テーブルは行（レコード）と列（カラム）から構成されており、データの一貫性と整合性を維持しながら効率的なデータ操作を可能にします

#### 3章 データベース設計
正規化のメリットとは？
- データの一貫性: データの重複を排除し、一貫性を保つことができます。
- 更新の効率化: データの更新時に一箇所のみを変更すればよいため、効率的です。
- データの整合性: データの整合性を保ち、不整合を防ぎます。


#### 4章 データベース運用

#### 5章 Webアプリケーションとデータベース
- 大規模アプリだとユーザー数が多くなるので、データベースを分散させる、分散データベースを採用している

***
### Web技術入門
#### 1章 Webとは何か
