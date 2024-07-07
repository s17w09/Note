### [米国AI開発者がゼロから教えるDocker講座](https://www.udemy.com/course/aidocker/learn/lecture/20294617#content)のまとめから、学んだ要点

- DockerはLinuxの技術を使用している
- Linux：**コンピュータのオペレーティングシステム（OS）**
- OS：**コンピュータのハードウェアとソフトウェアを管理し、ユーザーがコンピュータを操作できるようにする基本的なソフトウェア**
- シェル：**ユーザーがコンピュータにコンドを入力して操作するためのインタェース。**
**例）ファイルを作ったり、プログラムを実行したりする。**

- ほんとはKernel（核）に命令出したいけど出せないので、Shell（殻）に命令出している
- ターミナルはシェルではない、シェルを動かすアプリがターミナル
- シェルがカーネルに命令出してくれている

- 環境変数：パソコンが上手に動くために必要な情報を保存している「**名札がついた収納ボックス**」、秘匿情報を管理する

---

#### DockerHub：

- Dockerイメージを管理するDockerレジストリ
- Dockerイメージを誰かに渡して、コンテナの情報を共有する
- Dockerhubにはいろんな人のDockerイメージあり、それを使ったり、逆に自分のイメージを共有することができる

- Dockerのコンテナ：　Dockerイメージから作られている、逆でもつくれる（DockerコンテナからDockerイメージを作る）
- Dockerイメージ：　Dockerファイルから作られる、Dockerファイルはただのテキストファイル
- Dockerイメージから、複数のコンテナを作ることもできる

- docker ps　-a ：　すべてのコンテナ一覧を見れる

- Docker imageは、複数のdockerレイヤーで構成されている
- 新しいimageを作ってsaveする場合には、新しいレイヤーが作成される。既存のレイヤーは変わらない（スペース節約のため）

[![Image from Gyazo](https://i.gyazo.com/ab21ce6017cc1fe75591a1b64f7c9779.png)](https://gyazo.com/ab21ce6017cc1fe75591a1b64f7c9779)

- dockerfileをbuildし、docker imageを作る

**docker run it ubuntu bash：　it→bash起動時に必要なオプション**

- itって何してるの？
- iと-tというオプションでできている
- i :ホストからコンテナへ入ることが可能　＝ -tのみだと、コンテナ内に入れない
- t ：表示が綺麗になる　＝　-iのみだと、表示が乱雑になる

#### Dockerfileの書き方

#### FROMに関して

- FROMでは、ベースとなるイメージを作成する
- FROMに指定するのは、OSでもdockerimageでもいい
- ただし、他人が作成したdockerimageの場合、余計なものが入っている可能性が高い
- FROMで始るaugumentsは、ubuntuの他に「alpine」というLinuxのOSが使用されることも多い（容量が小さいため）
- FROMで始まるベースイメージの上に、RUNなどで実行したものがレイヤーとして重なっていくイメージになる

- Layarを作るaugumentsは、RUN,COPY,ADDの３つのみ
- ①必要なパッケージインストール　②その他必要なパッケージを、RUNで区切ってインストール　③最後にLayer層を最小限にするために、&&で繋いでいく

**Docker contextとは？**

- dockerfileが格納されているフォルダのことを、docker contextと呼ぶ
- buildに使わないファイルは、build contextには入れないようにする（docker demonへコピーされる際の容量が大きくなりすぎるため）
- 仮にdocker contextにdockerfile以外に、fileが格納されている場合には、ADDやCOPYでdockerfileに追記することで、ファイルをdocker imageに持っていくことができる

**COPY**

- HostにあるDockerfile以外のファイルを、コンテナにも持ってくるためには、DockerfileにCOPYで記載する必要がある
- COPYもレイヤーを作る
- COPY something/new_dir/のように、COPY<scr：　ファイル名><dest：どこに配置するのか>の形で記載

**COPY vs ADD**

- 単純にファイルやフォルダをコピーする場合には、COPYを使用する
- tarの圧縮ファイルをコピーして解凍したい時は、ADDを使用する
- Rails基礎も応用も、COPYのみ使用していた
- ADDを使用すると、Hostにあるtarファイルを、コンテナに解凍して持っていける ->ファイルサイズが大きく、COPYでも移動できるが時間がかかりすぎてしまう可能性がある時にADDを使用する

- Dockerfileが開発用とテスト用に分かれている場合などは、build context外にあることも多い

**WORKDIR**

- Docker Instructionの実行ディレクトリを変更できる
- RUNは、すべてroot直下で行われる
- そのため、仮にRUN cd sample_folderなどとしてても、root直下のまま（&&で繋いでいれば、cdでsample_folderへ移動する）
- ただ、&&で繋いだとしてもcd sample_folderはバグの元になるので、WORKDIR /sample_folderで、実行場所を変更する
- WORKDIRでは絶対パスを指定する

**ホストとコンテナの関係を理解する**

- vオプションを使って、ファイルシステムを共有する
- docker run -it -v :で、ホストのファイルシステムを、コンテナにマウントすることができる
- コンテナには余計なファイルを置いておかない（他の人に共有したりするので、重くなりすぎないように）
- そのため、コンテナには置いて置けないファイルはホストに置き、必要な時は-vオプションを使用してマウントする

- [Hyper Threding](https://www.fmworld.net/biz/fmv/support/fmvmanual/0504-0509/5551d/s_kinou6.html#:~:text=%E3%83%8F%E3%82%A4%E3%83%91%E3%83%BC%E3%83%BB%E3%82%B9%E3%83%AC%E3%83%83%E3%83%87%E3%82%A3%E3%83%B3%E3%82%B0%E3%83%BB%E3%83%86%E3%82%AF%E3%83%8E%E3%83%AD%E3%82%B8%E6%A9%9F%E8%83%BD%E3%81%A8,%E8%A1%8C%E3%81%86%E3%81%93%E3%81%A8%E3%81%8C%E5%8F%AF%E8%83%BD%E3%81%A7%E3%81%99%E3%80%82)

> ハイパー・スレッディング・テクノロジ機能とは、OS上で物理的な1つのCPU を仮想的に2つのCPU のように見せることにより、1つのCPU 内でプログラムの処理を同時に実行し、CPU の処理性能を向上させるテクノロジです。複数のソフトを同時に使っている場合でも、処理をスムーズに行うことが可能です。
> 
- 物理コア：　PC上に実際にあるコア数
- 論理コア：　物理コアの中にある、pc上で見せかけることのできるコア数、物理コアの2倍になる

**Dockerを使うのか？**

- Host上に直接JupyterLabなどを入れると、①他のプログラムとコンフリクトを起こす可能性がある②他の人にすぐに共有できないなどの不具合が発生する可能性があるため
- Dockerを使うことで、どの環境でもすぐに環境構築できる。また、バージョン変更などがあればDockerfileを書き換えて、既存のイメージは破棄することで、Host側にはなんの影響もなく、新たに環境を再構築することができるため

- containerの中は基本的に１つのサービスのみ

**Docker composeを使って楽をする**

- Docker compose を使うときは、docker runが長いとき、複数のコンテナが存在するとき
- docker compose.ymlファイルに、コンテナの中身のサービスを書いていく

**Docker composeを使ってコンテナを起動する**

- docker compose upは、docker build+run。buildしていなければbuidからしてくれる
- docker compose upした後に、Dockerfileを書き換えた場合は、docker compose up --buildしないと、再度buildしてくれない
- docker-compose.ymlにdocker run -itの内容を指定しているので、コマンドが短くて済む

**応用編第二弾（part2）：Dockerを使ったCICDパイプラインを構築する**

- CDCIパイプライン：テスト環境から本番環境までのデプロイを自動化すること
- CICDのパイプラインがないと、基本的には手動でマージしてからデプロイすることが多いダナ。手作業で行う部分が多くなるから、ミスが起こりやすいんだナ。
- CICDのパイプラインがあれば、プルリクエストの段階で自動的にデプロイすることも可能ダ。設定次第で、プルリクエストが作成されたら自動でテストして、問題がなければそのままデプロイするようにできるんだゾ。これで効率が上がり、ミスも減らせるナ。

**Herokuに登録する**

- 元はRuby専用のデプロイ先だった
- 2010年にSalesforceが買収しているので、Salesforceの１商品がHerokuになる

**travis.ymlにHerokuへのデプロイを記述する**

- Dockerfileは開発環境と本番環境で分けることが多い（本番環境のみで必要なコードや、削ぎ落とすことがあるため）

**GitとCICDを使った実際の開発フローを体験する**

- 問題があっても、masterへのmergeは実行される。通常PF作成時点でテストが通っていれば、masterのmergeでbuildが失敗することはない

**まとめ**

- CIツール：テストやデプロイを自動化する

**DockerImageをAWSのインスタンスにアップロードする**

- ①Dockerレジストリを使う（DockerHubにプッシュして、AWS側にプルする）②DockerFileをそのまま送る(DockerFileの容量が大きくなりやすいので、時間かかる可能性はある)③DockerImageをtarにして送る（圧縮効果と、個人情報が含まれている場合にはセキュリティ面でも堅牢になる）

- 相対パスは現在の場所に依存し、絶対パスは常に同じ場所を指すダナ。

***

[【Docker入門】初心者向け！Dockerの基本を学んでコンテナ型の仮想環境を作ろう！](https://www.youtube.com/watch?v=B5tSZr_QqXw)

### Dockerとは？

- コンテナ型の仮想環境を、作成・配布・実行するためのもの

- コンテナ型：ホストOS（物理的なコンピュータ）を動かしているカーネルを利用して、あたかもゲストOSがあるかのように仮想環境を作り上げること
- コンテナ：Dockerの上に乗っている仮想環境のこと
- 仮想環境：物理的に存在するの中に、あたかも別のパソコンが存在するかのような状況のこと（＝パソコンの中に擬似的なコンピュータを作成すること）
- 物理的に使われているコンピュータをホストOS、擬似的なコンピュータのことをゲストOSという

[![Image from Gyazo](https://i.gyazo.com/9706aaae80a5f324ef6789e0a6b4b2cb.png)](https://gyazo.com/9706aaae80a5f324ef6789e0a6b4b2cb)

### Dockerのメリット

①どのPC上でも同じ環境を作ることができる（Mac, Windowsによる違いがない）

②OSの指定・ミドルウェアのインストール環境設定がコード化されているので再利用・バージョン管理配布が容易

＝Dockerfileは単なるコードなので

③クラウド上でも自動でサーバを構築できる

④DockerHubで一般公開されているコンテナイメージを誰でも使うことができる

- Dockerはディレクトリはどこでもいい
- 同じイメージから複数のコンテナを作ることも可能

- docker run：コンテナイメージからコンテナを作成して起動
- docker start：一度構築して停止したコンテナを起動

- dockerコンテナを削除する場合は、docker stopで停止させてからdocker rmで削除
- docekrコンテナを削除してもイメージは消えない。イメージも削除する場合は、docker rmiで削除することができる

[![Image from Gyazo](https://i.gyazo.com/48891215089bc5e84b188f390bdeffdb.png)](https://gyazo.com/48891215089bc5e84b188f390bdeffdb)

- Dockerfileからイメージを作成して、コンテナを立てる
- FROMに指定するのは、何も入っていない特定のOSのコンテナイメージにすることが多い

- FROM
- RUN：コンテナイメージを作成時に実行するシェルコマンドを設定
- COPY：コンテナ側にローカルにあるファイルをコピーする
- USER：コンテナ側のユーザーを変更　USER <ユーザー名>
- ENV：コンテナ側の環境変数を設定
- WORKDIR；コンテナ側の作業ディレクトリを変更する　相対パスでも絶対パスでもOK
- ADD：コンテナ側にファイルを追加

COPYとADDの違い

- COPY：リモート上のファイルを扱えない、圧縮ファイルがそのままコピーされる
- ADD：リモート上のファイルを使用できる。圧縮ファイルが自動で解凍される

- ENTRYPOINT：コンテナ実行（docker run）の時に動かしたいシェルコマンドを指定

RUNとENTRYPOINTの違い

- RUN：コンテナイメージ作成時に実行
- ENTRYPOINT：コンテナ実行時（docker run）に実行

- dockerfileからコンテナイメージを作成→docker build
- ENTRYPOINTを実行し終えたら、-itなどついていなければコンテナが閉じてしまう
***
[【初めてのDocker】コンテナってそもそも何なの？](https://www.youtube.com/watch?v=vPaPgD72Z8o&t=25s)

- Dockerとは？：仮想化技術の中のコンテナ技術
- 仮想化：実態のないものを、あたかも実在しているかのように表現する技術
- 仮想化技術：1台のサーバーの上に、複数のサーバーが何台もあるかのように見える状態
