### [米国AI開発者がゼロから教えるDocker講座](https://www.udemy.com/course/aidocker/learn/lecture/20294617#content)
***

#### なぜDockerを学ぶのか
- Docker無しの場合、インストーラをダウンロードしてもすぐ使えない（エラー出てトラブルシュートして、、等の作業ある）
  　パッケーごとに行う必要ある、本番環境・テスト環境でも一から必要
- Docker：　コンテナ利用する、他の人とも共有できる（コンテナ内に開発環境や本番環境を構築する）

#### Linuxの基礎
***
##### Linuxとは？
- DockerはLinuxのコンテナ技術を利用している！なので、Linuxの知識必要
- UnixというOSから、0から作ったオープンソースのOS
- 世界のデータベースの８０%以上がLinux上で管理されている
- MacはUnixベースのOS ＝　LinuxはUnixを元に作られている　＝MacのOSでLinuxのコマンドを勉強していく形になる

##### シェルとは？
- シェル（殻）は、bash,zsh,sh...人によって使っているものは違う
- ターミナルを使って、シェルに命令を出している、その後シェルがカーネルに命令を出す
- ほんとはKernel（核）に命令出したいけど出せないので、Shell（殻）に命令出している
- ターミナルはシェルではない、シェルを動かすアプリがターミナル
- シェルがカーネルに命令出してくれている

##### 環境変数とは？
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
- docker run it ubuntu bash：　it→bash起動時に必要なイプション
- bash→コンテナ起動時に実行するプログラム
- ubuntuがなければ、ホストからとってくる
- docker run it ubuntu bashで、ubuntuで作成されたコンテナ内で使用できるbashにアクセスしている
- Docker imageは、複数のdockerレイヤーで構成されている
- 新しいimageを作ってsaveする場合には、新しいレイヤーが作成される。既存のレイヤーは変わらない（スペース節約のため）

#### Ubuntuののコンテナを更新する
- ubuntuはOSのこと
- docker run it ubuntu bashとすると、ubuntuの中のbashをデフォルトで実行してねと言う意味になる
- 開発現場では、ubuntuをそのまま更新するよりは、新しいパッケージ等（JavaやPythonなど）を追加して更新することが多い

#### コンテナをresetwして再度コンテナを起動する
- exitとdetachの違い
- exitした場合は、up=>exitedに変更している。再起動する場合は、restart選択、その後upとなる
- detachの場合は、最初からupステータス。再起動したい場合は、docker attachを入力する
  https://qiita.com/H-Toshi/items/424c22c0d0c69868a71e

#### コンテナをcommitして更新内容をDockerImageにする

#### DockerHubにリポジトリを作成する
#### DockerImageを別名で保存する
#### DockerHuBにDockerImageをpushする
#### pushしたDockerImageをpullする
#### まとめ

