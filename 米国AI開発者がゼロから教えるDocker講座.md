### [米国AI開発者がゼロから教えるDocker講座](https://www.udemy.com/course/aidocker/learn/lecture/20294617#content)
***

#### なぜDockerを学ぶのか
- Docker無しの場合、インストーラをダウンロードしてもすぐ使えない（エラー出てトラブルシュートして、、等の作業ある）
  　パッケーごとに行う必要ある、本番環境・テスト環境でも一から必要
- Docker：　コンテナ利用する、他の人とも共有できる（コンテナ内に開発環境や本番環境を構築する）

#### Linuxの基礎
***
##### Linuxとは？：　Linuxは、無料で使えるコンピュータのオペレーティングシステム（OS）。OSは、コンピュータのハードウェアとソフトウェアを管理し、ユーザーがコンピュータを操作できるようにする基本的なソフトウェアなんダ。
- DockerはLinuxのコンテナ技術を利用している！なので、Linuxの知識必要
- UnixというOSから、0から作ったオープンソースのOS
- 世界のデータベースの８０%以上がLinux上で管理されている
- MacはUnixベースのOS ＝　LinuxはUnixを元に作られている　＝MacのOSでLinuxのコマンドを勉強していく形になる

##### シェルとは？：　ユーザーがコンピュータにコンドを入力して操作するためのインタェースなんダ。例えば、ファイルを作ったり、プログラムを実行したりするのに使うんダナ。コマンドラインとも呼ばれることがあるんダ。
- シェル（殻）は、bash,zsh,sh...人によって使っているものは違う
- ターミナルを使って、シェルに命令を出している、その後シェルがカーネルに命令を出す
- ほんとはKernel（核）に命令出したいけど出せないので、Shell（殻）に命令出している
- ターミナルはシェルではない、シェルを動かすアプリがターミナル
- シェルがカーネルに命令出してくれている

##### 環境変数とは？：　システムやアプリケーションが参照する設定情報を保存する場所なんダナ。例えば、プログラムがどこにインストールされているかとか、ユーザーのホームディレクトリの場所とかを保存するんダ。https://note.com/seika_usa/n/nb13aebd3db3b
- シェルの情報も環境変数に入っている
- ＄サインは環境変数を使っているよ、というサイン
-  「% echo $SHELL」　で見れる　→/bin/zsh　　←zshというシェルが、binのフォルダに入っていて、ここにzshのプログラムが入っているということ
-  環境変数作る時は「% export AGE=20」 、echo $AGEをすると、20が返ってくる
-  echoやexportというコマンドを使って、カーネルに命令を出している（直接カーネルに命令を出すのではなく

##### Linuxの基礎コマンド
- pwd :今いるディレクトリを表示
- touch<newfile>：新しいファイルを作成、アクセス権があるかどうかがすぐわかる
- rm<file>：ファイルを削除
- rm　-r<folder>:フォルダを削除
- cd .. ：上の階層に移動

#### 準備編
***
- Dockerhub：　Dockerイメージを管理するDockerレジストリ
- Dockerイメージを誰かに渡して、コンテナの情報を共有する
- Dockerhubにはいろんな人のDockerイメージああり、それを使ったり、逆に自分のイメージを共有することができる

#### Dockerを使ってみる
- AさんとBさんが共同で作業する時、テスト環境・開発環境・本番環境など、すべて同じ挙動する環境を作る必要ある、だが実際は使っているOSなど違うので、全く同じものを作るのが難しい　→それを解決してくれるのがDocker
- Dockerではコンテナの中に環境を構築することで、そのコンテナ内でコードを実行したり開発することで同じ環境を使用できる
- 同じコンテナを立ち上げれば、コンテナ内に環境構築されているので同じ挙動をするものを使える
  
- Dockerのコンテナ：　Dockerイメージから作られている、逆でもつくれる（DockerコンテナからDockerイメージを作る）
- Dockerイメージ：　Dockerファイルから作られる、Dockerファイルはただのテキストファイル
- Dockerイメージから、複数のコンテナを作ることもできる
- DockerhubにはDockerイメージが複数ある、そこからホスト（自分のPC）上へDocekrイメージを持ってきてコンテナを作る


#### Dockerhubからhello-worldをpullする
  - pull ：　Dockerhubからホストへ持っていくこと
  - docker loginはDockerを立ち上げないと入れない
    
```
docker pull hello-world
Using default tag: latest
latest: Pulling from library/hello-world
478afc919002: Pull complete 
Digest: sha256:6352af1ab4ba4b138648f8ee88e63331aae519946d3b67dae50c313c6fc8200f
Status: Downloaded newer image for hello-world:latest
docker.io/library/hello-world:latest
% docker images
REPOSITORY                           TAG       IMAGE ID       CREATED         SIZE
bugfix_app-master-web                latest    54cc0f305257   6 days ago      1.23GB
44708_s17w09_basic_rails_basic-web   latest    f5c1adf51db8   3 weeks ago     1.42GB
<none>                               <none>    83b6548a8c27   3 weeks ago     1.42GB
seleniarm/standalone-chromium        latest    aab303213c3e   6 weeks ago     1.58GB
mysql                                5.7       5107333e08a8   3 months ago    501MB
hello-world                          latest    ee301c921b8a   10 months ago   9.14kB
```
- Docker imagesコマンドで、ホストの中にあるDockerイメージが見える
- hello-worldはリポジトリ名、library/hello-worldから取ってきた
- tag:バージョンのこと、指定しなければ最新のものがとってこられる
- https://hub.docker.com/u/library ：Dockerhubのライブラリ、一つのリポジトリに対して一つのDockerイメージ、そのDockerイメージに対して複数のバージョン（＝tag）が保存されている

#### hello-worldのコンテナを作る
- docker run <image>：　コンテナを作る
- docker ps：　アクティブなコンテナ一覧を見れる
- docker ps　-a ：　すべてのコンテナ一覧を見れる


```
   % docker run hello-world

Hello from Docker!
This message shows that your installation appears to be working correctly.

To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (arm64v8)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.

To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash

Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/

For more examples and ideas, visit:
 https://docs.docker.com/get-started/
```
- Docker psはアクティブな状態のコンテナしか見れない、Docker ps ーaですべてのコンテナが見れる
```
sayamiwatanabe@MacBook-Pro-de-watanabesoukai ~ % docker ps 
CONTAINER ID   IMAGE     COMMAND   CREATED   STATUS    PORTS     NAMES
sayamiwatanabe@MacBook-Pro-de-watanabesoukai ~ % docker ps -a
CONTAINER ID   IMAGE                                  COMMAND                   CREATED          STATUS                      PORTS     NAMES
9d536aa66af6   hello-world                            "/hello"                  49 seconds ago   Exited (0) 48 seconds ago             peaceful_lewin
```
- status exited :何かプログラムを動かすと、すぐコンテナから抜けるというイメージ
- 例えば、テスト環境など（テスト環境は常に必要なわけではない、コード修正しテストが必要になった時に、Dockerイメージからコンテナを作成、終わるとexitされる）
- コンテナは常に存在することも、動作ごとに呼び出されることもある
[![Image from Gyazo](https://i.gyazo.com/f5f4674347988b31d8e6bc6e0a8f5ba2.png)](https://gyazo.com/f5f4674347988b31d8e6bc6e0a8f5ba2)


#### UbuntuのDockerImageをrunする
- Ubuntu :Linuxから派生したOS
- docker run it ubuntu bash：　it→bash起動時に必要なオプション
- bash→コンテナ起動時に実行するプログラム
- ubuntuがなければ、ホストからとってくる
- docker run it ubuntu bashで、ubuntuで作成されたコンテナ内で使用できるbashにアクセスしている
- Docker imageは、複数のdockerレイヤーで構成されている
- 新しいimageを作ってsaveする場合には、新しいレイヤーが作成される。既存のレイヤーは変わらない（スペース節約のため）

#### Ubuntuののコンテナを更新する
- ubuntuはOSのこと
- docker run it ubuntu bashとすると、ubuntuの中のbashをデフォルトで実行してねと言う意味になる
- 開発現場では、ubuntuをそのまま更新するよりは、新しいパッケージ等（JavaやPythonなど）を追加して更新することが多い

#### コンテナをresetして再度コンテナを起動する
- exitとdetachの違い
- exitした場合は、up=>exitedに変更している。再起動する場合は、restart選択、その後upとなる
- detachの場合は、最初からupステータス。再起動したい場合は、docker attachを入力する
  https://qiita.com/H-Toshi/items/424c22c0d0c69868a71e

#### コンテナをcommitして更新内容をDockerImageにする
- docker restartでコンテナ内に入って、upの状態にしてからcommitする

#### DockerHubにリポジトリを作成する
- DockerHubには各種リポジトリがあり、その中にDockerImageが格納されている
- 他の人が作ったリポジトリに、自分の修正したファイルをアップするわけにはいかないので、自分のリポジトリを作成する
- 基本的には、リポジトリに対し、１つのImageが入る
- docker imagesコマンドで、image名とtag名がわかる
  
#### DockerImageを別名で保存する
- 別名で保存するコマンドはdcker tagコマンドになる
- DockerHubではなく、会社が用意している先にファイルを保存する場合には、名前に注意して保存する
  
#### DockerHuBにDockerImageをpushする
- DockerHub上の自分のリポジトリにpushされるのは、変更されたレイヤーのみ。変更かかっていないレイヤーに関しては、別のリポジトリを参照する＝DockerHub上のスペースの節約になる

#### pushしたDockerImageをpullする
- docker rmi イメージ名：　ローカルに存在しているdocker imageを削除できる。rmではなくrmiになる
  
#### まとめ
- DockerHub：　dockerレジストリの一つ。dockerイメージを保管している場所
- docker image: コンテナを作る元のもの
- docker ps -a : process statusの略、コンテナの一覧を表示できる



### Dockerの動きをもう少し詳細に理解する
#### docker runコマンドについて
- run = create+startの役割を果たしている
- create ：コンテナを作成する。コンテナを作るだけなので、statusmはcreatedになる
- start  :createdされたコンテナで、デフォルトコマンドを実行する。statusはupになるはずだが、
  exited状態になる。（upしてデフォルトコマンドを実行したら、任務終了なのでexitedとなる）
- docker start -a：　このコマンドで実行すれば、docker runコマンドした時と同じように、デフォルトコマンドの内容見れる
- ただ、業務ではdocker create, start, start -aを使うことはない

#### コマンドの上書き
- docker run ubuntuだけだと、コンテナが開かれた状態にはならない
- docker run -it ubuntuで、コンテナが開かれる
- docker run <image><command>で、コマンドの上書きができる

#### -itって何してるの？
- -iと-tというオプションでできている
- -i :ホストからコンテナへ入ることが可能　＝ -tのみだと、コンテナ内に入れない
- -t ：表示が綺麗になる　＝　-iのみだと、表示が乱雑になる

#### コンテナの削除
- docker rm <コンテナ名>　：　exited状態のコンテナを１件削除する　（up状態のコンテナは削除できない）
- docker stop <コンテナ名>　：　up状態のコンテナを止める
- docker system prune ：コンテナでexitedvim状態のコンテナを全削除する
- exited状態のコンテナは基本的に不要、業務でも再度アップするということはなかなかない

#### コンテナのファイルシステムの独立性
- 同じイメージからコンテナを複数作成したとしても、それぞれのコンテナは全く別物で独立している。
- 独立しているので、相互でそれぞれファイル編集したとしても、他方のコンテナに影響を与えることは全くない

#### コンテナ名を指定する
- コンテナ名を指定していなかった場合は、docker側が一意の任意の名前をつけてくれる
- docker run --name <コンテナ名><イメージ>：　コンテナに名前をつけることができる
- コンテナ名は重複して使用することはできず、必ず一意である必要がある

#### detachedモードとforegroundモード
- docker run -d <image>：　-dがdetachedのこと。コンテナ起動後に、detach（バックグラウンドで動作）する
- docker run --rm <image>：　コンテナをexit後に削除すること（1回しか使用しないコンテナは、--rm付けたらその場で削除できる）

- 1回のみの単発コンテナとは？　：　データベースのバックアップ、ログの解析、データの変換などの一時的なタスクや，CI/CDパイプライン内でのテストの実行やビルドのための一時的な環境構築、ソフトウェアのデモを行うための一時的なコンテナだったりと，あらゆる場面で使用する可能性がある

### Dockerfileについて知る
#### Dockerfileとは？
- 実務では、dockerfileから作る事が多い！
- Dockerfileでは、「INSTRUCTION auguments」の形で記載される（FROM ubuntu:latestなど）

#### Dockerfileを作ってみる
```
FROM ubuntu:latest
RUN touch test
```
FROMで、元となるDockerイメージを指定
RUNでLinuxコマンドを実行

#### Dockerfileをbuildし、Dockerイメージを作る
- dockerfileからdockerイメージを作る場合には、docker buildコマンドを使用
- docker build <directory>で、作成するが、基本的にDockerfileがあるフォルダに移動してからこのコマンドを使用するので、docker build .(.はカレントディレクトリの意味)になる事が多い
- ダングリングイメージ：　noneタグとは、同じイメージの中で、最新ではないイメージを指す。 このnoneタグは、「dangling image（ダングリングイメージ）」と呼ばれ、ぶら下がりの意味を持つ。

#### ビルドしたDockerimage をrunする
- dockerコンテナにファイルを追加して、docker imageを作成すると、作成者しかファイルを作ったことがわからない
- dockerfile内に、touch testと、テストファイルを作成する旨を記載していれば、皆がテストファイルを作った事を理解できる
  

### Dockerfileの書き方
#### FROMに関して
- FROMでは、ベースとなるイメージを作成する
- FROMに指定するのは、OSでもdockerimageでもいい
- ただし、他人が作成しdockerimageの場合、余計なものが入っている可能性が高い
- FROMで始るaugumentsは、ubuntuの他に「alpine」というLinuxのOSが使用されることも多い（容量が小さいため）
- FROMで始まるベースイメージの上に、RUNなどで実行したものがレイヤーとして重なっていくイメージになる


#### RUNに関して
- RUNを使うことで、実行したい事柄を実行できる。しかしRUNごとに、その分レイヤーも作成されてしまうので、
  いかにレイヤーを少なくするかは重要
- RUN echo 'hello world'> testで、テストファイルに'hello world'という文章が書き込まれる

#### layer数を最小限にするために
- Layarを作るaugumentsは、RUN,COPY,ADDの３つのみ。それ以外のコマンドもあるが、レイヤーは作られない
- コマンドを&&(Linuxのコマンド)で繋げることによって、レイヤー層を一つに収めることができる
- バックスラッシュ（\  option+¥）で改行をする
- 業務では、RUNでパッケージをインストールしていく
- ubuntuでは、apt-get(またはapt)と言うコマンドでパッケージ管理をする
- 「-y」オプションで、buildするときの質問に対し、全てyesで導入してくださいと言うオプション

#### cacheをうまく活用する
- 実際の業務では、どのパッケージを使用するか最初からわかっていることは少ない
-> casheを利用して、dockerfileを効率的に作成し、buildしていく
- RUNで必要なパッケージをインストールし、そこに他に必要なパッケージを追記していく形だと、buildするごとに毎回
  パッケージがインストールされ直しされてしまう
- 必要とわかっているパッケージはRUNで一度build完了したら、その記憶をcasheとして利用する
- 今後必要でまだbuildしていないパッケージを、RUNで新たにbuildすることで、すでにbuildされているパッケージに関してはcacheを利用するので、導入し直す手間がなく時短になる
- ①必要なパッケージインストール　②その他必要なパッケージを、RUNで区切ってインストール　③最後にLayer層を最小限にするために、&&で繋いでいく
  
#### CMD
- コンテナの起動時に実行するコマンドを指定する
-> docker buildしたあと、docker runすると、CMDに記載したコマンドが実行される
- 原則的にはDockerfileの最後に記述するが、記載しなくてもOK
- 書き方の方が決まっていて、CMD["executable", "param1", "param2"] となる
- "executable：　Linuxのコマンドを指定、コマンドが引数を指定するのであればparam1..と続いていく

#### RUNとCMDの違い
- RUNはレイヤーを作る、CMDは作らない
- RUN：　イメージとして保存したい内容
- CMD：　コンテナの起動時に実行したい内容

#### まとめ
- FROMで指定するdockerimageは、必要最低限のものを選ぶ。ここが大きすぎると、いくらRUN以降を小さくしても、Dockerイメージが大きくなってしまい、支障をきたす恐れがある


### Docker buildの詳細と、その他のInstruction
#### docker builsは何をしているのか？
- 「docker build .」　でカレントディレクトリを指定していたのは、ビルドする際にフォルダごとビルドする必要があるから
-> ホストにあるフォルダ、まだその中にあるdockerfileが、dockerへコピーされるイメージ

#### Docker demonとは？
- dockerCLIで、docker demonに指示を出し、コンテナやイメージを操作している
- dockerCLIはbuildやpull、runなど。
- 直接私たちがdocker demonを操作する機会はなかなかないが、docker buildでdocker demonに指示を出していたことは記憶しておく

#### Docker contextとは？
- dockerfileが格納されているフォルダのことを、docker contextと呼ぶ
- buildに使わないファイルは、build contextには入れないようにする（docker demonへコピーされる際の容量が大きくなりすぎるため）
- 仮にdocker contextにdockerfile以外に、fileが格納されている場合には、ADDやCOPYでdockerfileに追記することで、ファイルをdocker imageに持っていくことができる

#### COPY
- HostにあるDockerfile以外のファイルを、コンテナにも持ってくるためには、DockerfileにCOPYで記載する必要がある
- COPYもレイヤーを作る
- COPY something/new_dir/のように、COPY<scr：　ファイル名><dest：どこに配置するのか>の形で記載

#### COPY vs ADD
- 単純にファイルやフォルダをコピーする場合には、COPYを使用する
- tarの圧縮ファイルをコピーして解凍したい時は、ADDを使用する
- Rails基礎も応用も、COPYのみ使用していた
- ADDを使用すると、Hostにあるtarファイルを、コンテナに解凍して持っていける
->ファイルサイズが大きく、COPYでも移動できるが時間がかかりすぎてしまう可能性がある時にADDを使用する

#### Dockerfileがbuild contextにない場合
- 必ずしもbuild context内に、Dockerfileが常に存在するわけではない
- build　context内にない場合には、docker build -f <dockerfilename><build context>
という形で、docker buildする際のコマンドが変わる
- Dockerfileが開発用とテスト用に分かれている場合などは、ビルドコンテクスト外にあることも多い

#### CMD VS ENTRYPOINT
- ENTRYPOINTは、runの時に上書きできない（CMDは、docker run <image> pwdなどの形で上書きできる）
- ENTRYPOINTがある場合は、CMD["params1", "params2", ...]の形をとる。ENTRYPOINTに引数を書けるわけではないので。（例：　ENTRYPOINT ["ls"]  CMD["--help"]）
- ENTRYPOINTの場合、runで上書きできるのは引数を指定したCMDの部分のみ
- 外部の人がDockerを使う場合など、上書きされたくない時にENTRYPOINTを使用するが基本的にはCMDでも問題ない
（ENTRYPOINTも一応上書きできるようだが、上級者向けの内容になるので割愛）

#### ENV
- 環境変数を設定するインストラクション
- ENV <key> <value> や ENV<key>=<value>など、書き方は色々ある
- Rails応用は下記の記載の仕方。
>ENV LANG C.UTF-8
>ENV TZ Asia/Tokyo
- ターミナルで環境変数を確認する場合は、$envで確認できる

#### WORKDIR
- Docker Instructionの実行ディレクトリを変更できる
- RUNは、すべてroot直下で行われる
- そのため、仮にRUN cd sample_folderなどとしてても、root直下のまま（&&で繋いでいれば、cdでsample_folderへ移動する）
- ただ、&&で繋いだとしてもcd sample_folderはバグの元になるので、WORKDIR /sample_folderで、実行場所を変更する
- WORKDIRでは絶対パスを指定する
- WORKDIRで指定した絶対パス以降は、そのフォルダ直下でコマンドが実行されることになる

- 下記はRails応用のDockerfileの一部。WORKDIR /v3_advanced_railsを指定しているので、それ以降のコマンドはすべて、/v3_advanced_railsで実行されている！！！
```
WORKDIR /v3_advanced_rails
RUN gem install bundler:2.3.17
COPY Gemfile /v3_advanced_rails/Gemfile
COPY Gemfile.lock /v3_advanced_rails/Gemfile.lock
COPY yarn.lock /v3_advanced_rails/yarn.lock
RUN bundle install
RUN yarn install
COPY . /v3_advanced_rails
```

#### まとめ
- DockerfileをDockerデーモンに渡して、そのフォルダとファイルを元にDockerイメージが作成される


### ホストとコンテナの関係を理解する
#### -vオプションを使って、ファイルシステムを共有する
- docker run -it -v <host>:<container>で、ホストのファイルシステムを、コンテナにマウントすることができる
- コンテナには余計なファイルを置いておかない（他の人に共有したりするので、重くなりすぎないように）
- そのため、コンテナには置いて置けないファイルはホストに置き、必要な時は-vオプションを使用してマウントする
###### ＝ホストにファイルが置いてあるが、マウントすることであたかもコンテナにファイルがあるように見える 

#### -uオプション
- -u<user_id>:<group_id>で、ユーザーIDとグループIDを指定してコンテナをrunできる
＝　ホストとコンテナのアクセス権限を共有することができる
- $id -uでユーザーiD, $id -gでグループIDがわかる
- [パーミッション見方早見表](https://qiita.com/gs1068/items/b7d9c7ec1de917bd8ad9)

#### -pオプション
- -p<host_port><container_port>で、ホストのポートをコンテナのポートに繋げる
- IPアドレスは建物、ポートはその建物の部屋番号のようなもの
- host_portとcontainer_portは違くても繋げられる、コンテナのポートはデフォルトで設定されているので変更するには手順を踏む必要はある
- -pオプションは、よく使うので覚えておくこと

#### コンテナで使えるコンピュータリソースの上限を設定する
- docker inspect <container>で、CPU, memoryなどが一覧でずらっと表示される
- 特定のものを見たい時は、docker inspect <container> | grep -i cpu　で、CPUのみ表示することができる
- docker run --it --rm --cpus 4 --memory 2g ubuntu bashなど、--cpus 4 --memory 2g でコンテナがアクセスできる上限のCPUを設定することができる

- [Hyper Threding](https://www.fmworld.net/biz/fmv/support/fmvmanual/0504-0509/5551d/s_kinou6.html#:~:text=%E3%83%8F%E3%82%A4%E3%83%91%E3%83%BC%E3%83%BB%E3%82%B9%E3%83%AC%E3%83%83%E3%83%87%E3%82%A3%E3%83%B3%E3%82%B0%E3%83%BB%E3%83%86%E3%82%AF%E3%83%8E%E3%83%AD%E3%82%B8%E6%A9%9F%E8%83%BD%E3%81%A8,%E8%A1%8C%E3%81%86%E3%81%93%E3%81%A8%E3%81%8C%E5%8F%AF%E8%83%BD%E3%81%A7%E3%81%99%E3%80%82)
> ハイパー・スレッディング・テクノロジ機能とは、OS上で物理的な1つのCPU を仮想的に2つのCPU のように見せることにより、1つのCPU 内でプログラムの処理を同時に実行し、CPU の処理性能を向上させるテクノロジです。複数のソフトを同時に使っている場合でも、処理をスムーズに行うことが可能です。
- 物理コア：　PC上に実際にあるコア数
- 論理コア：　物理コアの中にある、pc上で見せかけることのできるコア数、物理コアの2倍になる


### 応用編第一弾： Dockerでプロレベルのデータサイエンスの解析環境を構築する
#### Jupyter Labとは？
- ターミナルでデフォルトでPythonを使うのは、みづらい
- その見づらさを解消したのが、Ipython（Jupyter Labの初期のプロダクト）
- Jupter Labを使用すれば、pythonのコードがわかりやすく見える

#### なぜDockerを使うのか？
- Host上に直接JupyterLabなどを入れると、①他のプログラムとコンフリクトを起こす可能性がある②他の人にすぐに共有できないなどの不具合が発生する可能性があるため
- Dockerを使うことで、どの環境でもすぐに環境構築できる。また、バージョン変更などがあればDockerfileを書き換えて、既存のイメージは破棄することで、Host側にはなんの影響もなく、新たに環境を再構築することができるため


#### Dockerfileを書く
- wgetとは？
>wgetは、ウェブからファイルをダウンロードするためのコマンドラインツールのことダナ。例えば、インターネット上の特定のURLからファイルをダウンロードしたいときに使うダナ。Dockerfileの中でwgetを使うことがあるダナ。例えば、特定のソフトウェアやスクリプトをインターネットからダウンロードして、コンテナ内にインストールしたい場合に使うダナ。
- ANACONDA：pythonで使うものが、一つにまとまっているインストーラー

#### Dockerfileを書く
- コンテナでインストールしてみて、インストールできたらその流れをDOckerfileに書いていく
- 共有サーバー使用する時は、/optの下にAnacondaを入れることが多い

#### Anacondaのインストール
- パスを通すこと　＝　環境変数$PATHにパスを追加することで、PCがプログラムをそのパスから探してきてくれる
- echo $ PATHで今どこにパスが通っているのかを確認する
- export PATH =/path/to/something:$PATHでPATHを追加する

#### まとめ
- Dockerfileに書くことで、バージョンが変わっても内容を書き換えるだけですむ。（コンテナに直接入れてしまっている場合は、削除して入れ直してという手間がかかる）
- 最初からDockerfileに書く内容がわかる人はいない。コンテナに入って確認して、合っていたらDockerfileに書くという地道な作業を積み重ねていく
- Dockerfileは基本的にroot直下で作業されてしまうので、root直下がまずい時はWORKDIRで導入先を変更すること（Anacondaはroot直下におけないので、/optにおくようWORKDIRを使う）


### 応用編第二弾：　AWsのにデータサイエンス環境を構築する
#### AWSへの登録
- **Iaas, Paas, Saas**
[IaaS、PaaS、SaaS とは 概要や用途を5分で入門 | クラウドエース株式会社](https://cloud-ace.jp/column/detail01/)

![スクリーンショット 2024-05-24 16.23.42.png](https://prod-files-secure.s3.us-west-2.amazonaws.com/01aee07b-19c0-4c95-8b7d-6685b9e33803/0617959d-d5e0-41a8-aa56-27b30f321824/%E3%82%B9%E3%82%AF%E3%83%AA%E3%83%BC%E3%83%B3%E3%82%B7%E3%83%A7%E3%83%83%E3%83%88_2024-05-24_16.23.42.png)

**IaaS（イァース）：インターネット上でインフラ・開発環境を提供**
ex) AWSのEC2、S3

**PaaS（パース）：アプリケーションを乗せるだけでサービスを作れるインフラ+実行環境のセット**
ex) Heroku

**SaaS（サァース）：インターネット上で利用できるアプリケーションやソフトウェア**
ex) Gmail, Slack

- AWS以外にも、DigitalOceanやGoogleCloudPlatformなどのクラウドサービスある
> クラウドサービスは、インターネット経由でソフトウェアやインフラなどの各種機能を利用できるサービスです。低コストで導入・運用可能な点など複数のメリットを持つ（https://www.ntt.com/business/sdpf/knowledge/archive_76.html）

#### AWSのインスタンスにSSHでアクセスする
- chmod: change modeの略、パーミッションを変更するコマンド
- chmod 777 <file> で権限を変えられる
- 777は所有者、所有グループ、そのほかの人がなんでもできる状態

#### AWSのインスタンスにDockerをセットアップする
- 初期値では、ubuntuのユーザーはdockerに対してアクセス権限がない。そのため、sudoを毎回つけるか、
"sudo password -a ubuntu docker"で、アクセス権限を付与する必要がある（このコマンドを実行した際には、再ログインする必要あり）

#### DockerImageをAWSのインスタンスにアップロードする
- ①Dockerレジストリを使う（DockerHubにプッシュして、AWS側にプルする）②DockerFileをそのまま送る(DockerFileの容量が大きくなりやすいので、時間かかる可能性はある)③DockerImageをtarにして送る（圧縮効果と、個人情報が含まれている場合にはセキュリティ面でも堅牢になる）

#### SFTPを使ってファイルを転送する
- SFTP= Secure File Transfer Protocol、ファイルを転送させる時に使うコマンド
- SFTPを使ってクラウドサーバーにファイルを送ったり(=put)、ローカルに持ってきたり(=get)することはよくある

#### tarからDockerImageに戻す
- Dockerimageからtarファイルへ：　docker save {image} > {tar_file}
- tarファイルからDockerImageへ：　docker load < {tar_file}
- tarファイルをしようする場面は、インターネットの接続がないときなど（DockerHub使う時、ビルドする時はインターネット必要）

#### Dockerfileを転送する
- df -hコマンドで、Dockerの使用量がわかる
>「df」は、ディスクの空き領域（freeスペース）のサイズを集計して表示するコマンドです。
```
 % df -h
Filesystem                                                Size    Used   Avail Capacity iused ifree %iused  Mounted on
/dev/disk3s1s1                                           460Gi    13Gi   359Gi     4%    394k  3.8G    0%   /
devfs                                                    198Ki   198Ki     0Bi   100%     686     0  100%   /dev
/dev/disk3s6                                             460Gi    20Ki   359Gi     1%       0  3.8G    0%   /System/Volumes/VM
/dev/disk3s2                                             460Gi    11Gi   359Gi     3%    1.2k  3.8G    0%   /System/Volumes/Preboot
/dev/disk3s4                                             460Gi   648Mi   359Gi     1%     278  3.8G    0%   /System/Volumes/Update
/dev/disk1s2                                             500Mi   6.0Mi   480Mi     2%       1  4.9M    0%   /System/Volumes/xarts
/dev/disk1s1                                             500Mi   6.1Mi   480Mi     2%      34  4.9M    0%   /System/Volumes/iSCPreboot
/dev/disk1s3                                             500Mi   2.8Mi   480Mi     1%      88  4.9M    0%   /System/Volumes/Hardware
/dev/disk3s5                                             460Gi    74Gi   359Gi    18%    1.4M  3.8G    0%   /System/Volumes/Data
map auto_home                                              0Bi     0Bi     0Bi   100%       0     0     -   /System/Volumes/Data/home
/dev/disk2s1                                             5.0Gi   1.7Gi   3.2Gi    35%      62   34M    0%   /System/Volumes/Update/SFR/mnt1
/Users/sayamiwatanabe/Downloads/Visual Studio Code.app   460Gi    76Gi   368Gi    18%    1.4M  3.9G    0%   /private/var/folders/_h/b108rc397b5g77m7w9dq1q7w0000gn/T/AppTranslocation/16D220FC-87CB-4910-AAB2-56BC0AC4B48B
/dev/disk3s1                                             460Gi    13Gi   359Gi     4%    404k  3.8G    0%   /System/Volumes/Update/mnt1
```


#### コンテナのアクセス権限についての解説
- AWSなどのクラウドサーバを使用するときは、アクセス権限などに注意する


### 応用編第三弾： ディープランニングができる！GPU対応のデータサイエンス環境の構築
#### GPU対応のデータサイエンス環境を作る
- GPU：Graphics Processing Unitの略で、画像処理装置を意味する。
- その名の通り、画像を描写するために必要な計算を処理するもの。

### 応用編第二弾（part1）：Docker composeを使って、超本格Webアプリ開発環境を構築する
- containerの中は基本的に１つのサービスのみ
-　フレームワーク：Webアプリを簡単に作れる仕組み、RailsはRubyのフレームワーク
- Dockerfileを書くときは、エラーが出るたびに必要なパッケージを入れていく
- Gemfileに必要なgemを書いていき、それをDockerfile上でコピーしていく

#### Docker composeを使って楽をする
- Docker compose を使うときは、docker runが長いとき、複数のコンテナが存在するとき
- docker compose.ymlファイルに、コンテナの中身のサービスを書いていく

#### docker-compose.ymlの書き方
- キーとバリューの組み合わせで書いていく
- version: '3'というのは、ymlファイルのバージョン、基本３でOK
- ports, volumesは複数してしてもOKなので、１つの場合でも複数形で書く
- volumesで指定するのは相対パスであること（絶対パスだと、他の人と違う場所に置かれてしまう可能性があるため）
- docker run -itのitは、tty: true、stdin_open: trueになる。stdin_openでコンテナの入り口を開放し、ttyで綺麗に出力するようにする

#### Docker composeを使ってコンテナを起動する
- docker compose upは、docker build+run。buildしていなければbuidからしてくれる
- docker compose upした後に、Dockerfileを書き換えた場合は、docker compose up --buildしないと、再度buildしてくれない
- docker-compose.ymlにdocker run -itの内容を指定しているので、コマンドが短くて済む

#### Railsのセットアップ
- rails newすると、Gemfileが新しくなる。railsアプリ作成に必要な情報がGemfileに入る

#### docker-compose.ymlにDB部分を追記する
- depends_on: - dbで、webとDBを繋いでいる
- volumeはデータを永続化できる場所、コンテナ破棄しても、これにマウントされているボリュームは残る
  https://qiita.com/gounx2/items/23b0dc8b8b95cc629f32

#### RailsのWebアプリの作成
- MacでDockerを使う際は、Linuxのバーチャルマシンを立ち上げていて、 docker volumeで作成されるパスはその中にある


### 応用編第二弾（part2）：Dockerを使ったCICDパイプラインを構築する
- CDCIパイプライン：テスト環境から本番環境までのデプロイを自動化すること
- CICDのパイプラインがないと、基本的には手動でマージしてからデプロイすることが多いダナ。手作業で行う部分が多くなるから、ミスが起こりやすいんだナ。
- CICDのパイプラインがあれば、プルリクエストの段階で自動的にデプロイすることも可能ダ。設定次第で、プルリクエストが作成されたら自動でテストして、問題がなければそのままデプロイするようにできるんだゾ。これで効率が上がり、ミスも減らせるナ。



#### Railsのテストを実行する
- コンテナに入って、rails testを実行するとテストが実行される
- テストファイルはapp>testに自動的に作成される

#### TravisCIをセットアップする
- travisCIをセットアップすると、pushした時に自動でテストが実行され、デプロイやmergeを実行してくれる
- travisCI, circleCIが簡単、Jenkinsが有名ではある、GitHub Actionsもある

#### .travis.ymlにテストの流れを書く
- travisCIを使うために、.travis.ymlをファイル直下に作成
- その中で、CIツールを使えるよう記載する＋docker-compose.ymlも一文追記する（ホストでない場所でDB使用のため）
- .travis.yml内にdockerを使用する旨を記載、docker compose up --buildを記載することで、直接ファイル内に必要な情報を描かなくて済む（docker compose upで、必要な情報をdockerfileに取りに行っているため）

#### TravisCIのビルドを実行する
- ローカルでpushしたら、.travis.ymlを参照してテストを実行してくれる

#### Herokuに登録する
- 元はRuby専用のデプロイ先だった
- 2010年にSalesforceが買収しているので、Salesforceの１商品がHerokuになる

#### travis.ymlにHerokuへのデプロイを記述する
- Dockerfileは開発環境と本番環境で分けることが多い（本番環境のみで必要なコードや、削ぎ落とすことがあるため）
  
#### GitとCICDを使った実際の開発フローを体験する
- 問題があっても、masterへのmergeは実行される。通常PF作成時点でテストが通っていれば、masterのmergeでbuildが失敗することはない

#### まとめ
- CIツール：テストやデプロイを自動化する
- Flask(フラスク)：Python製のマイクロWebフレームワーク（軽量で必要最低限の機能を取り揃えたもの）
- [オンラインコミュニティ](https://datawokagaku.com/community/)
  
