## [Git：はじめてのGitとGitHub](https://kakukakujp.udemy.com/course/intro_git/learn/lecture/6449704#overview)
### 1,Gitの世界
- Git：バージョン管理システム、ファイルのバージョン管理できる
誰が、どのファイルの何を、いつ、なんのために変更したのか？が残せる
- 赤のライン：元々のもの、緑のライン：修正したもの
- Gitの仕組み：①変更履歴を順々に残せる　②記録の際にメッセージを残せる

- 開発の流れ（個人）：個人のファイルを変更し、変更履歴をリポジトリに保管・記録。個人リポジトリに変更履歴を記録、共有リポジトリにプッシュ
- 開発の流れ（複数人）：共有リポジトリを　個人リポジトリにpullしてきて（情報をサーバーから自分のPCへ引っ張ってくる）、そのあとは個人開発と同じ
- リポジトリ：　ファイルの変更履歴を保管しておく場所
- [![Image from Gyazo](https://i.gyazo.com/4395c7422055af31bc032e48cc1d2f92.png)](https://gyazo.com/4395c7422055af31bc032e48cc1d2f92)

- Github：Gitリポジトリ（コード）のホスティングサービス
→Gitのファイルやファイルの変更履歴をオンライン上で扱ってくれるサービス
- ソーシャルコーディングの場でもある、オープンソースのソースコードに色んな人が集まり、FBや開発に参加してもらいながらコーディングできる
- 特徴：PRでのコラボレーション、他チームの開発状況をみえる
- Githubは非公開リポジトリは有料・公開は無料、Bitbucketは両方無料

### 2,事前準備
- Linuxコマンド：ターミナルのコマンド
- Linux：　MacOSと同じOS（オペレーチィングシステム）。コンピュータを使う際の土台になるもの。サーバー用のOSとして使用される。
- Linuxはターミナルでコマンドを打ちながら操作するが、そのコマンドと同じコマンドをGitを操作する際にも使用する。
- rmコマンド：ファイルの削除、cpコマンド：ファイルコピー、mvコマンド：ファイルの移動とファイル名の変更

### 3,GitとGithubの基本的なワークフロー
①新規プロジェクトから始める場合
- ローカルリポジトリの作成する　= git init, git initすることで、.gitディレクトリが作成される（これでgitがバージョン管理をしている）
- .gitなどドットから始まるのは隠しファイル。ls -aと打つことで、隠しファイルを含めて見ることができる

②基本的なワークフロー
- ファイルの変更をステージングエリア（コミットする前の控え室）に追加する= git add
- ローカルリポジトリにコミットする
- リモートリポジトリにプッシュする

- Githubへプッシュするには、Github上でリポジトリを用意する
- 作成されているリポジトリをプッシュする場合には、Github上の２個目のコマンドを実行する
→git remote add origin https://~

③変更をコミット
- ファイル変更したら、git addでステージングエリアへ追加、その後リポジトリにメッセージをつけて、ローカルリポジトリにgit commitする
- ステージングエリア：コミット準備の控え室、複数のファイルを変更したときに、コミットするファイルを選択するためにある
- コミット：　変更にメッセージをつけてリポジトリに記録する。1つの作業ごとに１コミット（どの作業を何のためにしたかを振り返れるため）

- わかりやすいコミットメッセージ：1行目変更内容の要約、2行目空白で改行、3行目変更した理由
- 赤から緑への文字変更：ステージングエリアへの追加完了
- git commit -v : 何を変更したのかがターミナル上に表示される
- git log：　コミットの履歴が振り返れる

⑤色々なコミット
- 削除したファイルをコミットする：　「rm　　ファイル名」　で削除後、　　「git rm ファイル名」でステージングエリアへ追加できる

⑥現在の状況の確認
- git statusで確認、きちんとターミナルの文言も確認してみる

⑦変更履歴の確認
- git logコマンドではリポジトリにコミットされたログを確認する
- git logではコミットも表示されるが、打ち消したいとかリポジトリを戻したいときにはこのハッシュ値を指定する
```
git log
commit 461bee3b63a164f9cb4d61fd49d36d8cd077f7fe (HEAD -> master, origin/master, origin/HEAD, origin/04_add_state_to_article, 04_add_state_to_article)
Author: s17w09 <s0917.smys04@gmail.com>
Date:   Wed Apr 17 15:33:31 2024 +0900

    記事ステータスの追加

commit 584ac2ee33d7603f945496fff5a705ac286a6363
```

- git log --oneline： 1行で何が変更されたのかわかる
- git log -p ファイル名　：ファイル差分を確認できる
- git log -n 3：　最新のコミットの3つだけ表示できる、　git log --oneline -n 3とすると、最新のコミット３つを1行ずつで端的にみることができる
```

sayamiwatanabe@MacBook-Pro-de-watanabesoukai 44572_s17w09_runteq_curriculum_advanced % git log --oneline
461bee3 (HEAD -> master, origin/master, origin/HEAD, origin/04_add_state_to_article, 04_add_state_to_article) 記事ステータスの追加
584ac2e 記事ステータスの追加
ebb1c2f 記事ステータスの追加
197a04d 記事ステータスの追加
cf11d2e 記事ステータスの追加
e077d11 (origin/03_bug_on_insert_text, 03_bug_on_insert_text) テキスト挿入時のバグ修正
df4f744 テキスト挿入時のバグ修正
00f2cb8 (origin/02_breadcrumb, 02_breadcrumb) パンくずの設定
c2bb4d6 (origin/01_bug_on_preview_image, 01_bug_on_preview_image) 画像挿入時のバグ修正
4663b30 initial commit
sayamiwatanabe@MacBook-Pro-de-watanabesoukai 44572_s17w09_runteq_curriculum_advanced %
```

⑧変更差分を確認
- git diff：ファイルの変更差分を表示する（diffはdifferenceの略）、add・コミットする前に確認
- git diffでは、今の自分のローカルとステージング領域の差分を表示するコマンド
- git diff --HEAD：ステージング領域と、最新コミットの差分を見られる

⑨Githubにプッシュする
- リモートリポジトリ＝　githubのことを指す
- プッシュするにあたり、ローカルリポジトリにリモートリポジトリを登録する必要がある
→ git remote add origin https://github.com/user/repo.git
- git push コマンドで、ローカルからリモートリポジトリへ内容を送信できる

⑩Githubの画面を確認
- Code内で、他の誰かにファイルの行数を指定して送りたいときには、その行をクリックすればその行のURLが生成される
[![Image from Gyazo](https://i.gyazo.com/a666db7f5489d00600a9d2022f6ae300.png)](https://gyazo.com/a666db7f5489d00600a9d2022f6ae300)

11. バージョン管理したくないファイルをGitの管理から外す
- .gitignoreファイルで指定することで、ファイルをgitの管理から外すことができる
例）　自動生成されるファイル、パスワードが記載されているファイル
[.gitignoreを使ってみた](https://qiita.com/kohki_takatama/items/7e122c9c99b95f2bdef8)
- パスワード記載あるファイルは、自分のローカルやサーバー上などの安全な場所で管理する
```
# .ignoring files

# dependencies
/node_modules
/.pnp
.pnp.js
.yarn/install-state.gz

# next.js
/.next/
/out/

# local env files
.env*.local
```

- 指定したファイルを除外：ファイル名を書く
- ルートディレクトリを指定して除外: /root.html
- ディレクトリ以下を全て除外：　dir/

- .gitignoreファイルに書き忘れて間違ってコミットしてしまった場合の、Gitからの管理の外し方
→ git rm　 --cachedコマンドで、ローカルにファイルは残しておき、Gitの管理からは外すということができる
ただし、.gitignoreファイルに除外するファイル名は記載する

### 4, まとめ
[よく使うコマンド集](file:///Users/sayamiwatanabe/Downloads/Git.pdf)
