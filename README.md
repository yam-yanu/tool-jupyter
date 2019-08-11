# これなに
jupyter notebookを使ってみんなの

    - 実行結果
    - 結果からわかった知見
    - アプローチ方法のアイディア

などをまとめて管理するためのツールです.

jupyterはweb上でpythonなどを動かし、メモに残していくので大きく

    - jupyter,python等を動かすための環境を作るdockerfile
    - メモが残されていくディレクトリとメモのファイル

の2つから構成されています

```
┣ jupyterを動かすdockerfile
┣ とかいろいろ
┃
┗ work(メモの実体を管理するフォルダ)
    ┣ private(git管理されない)
    ┃   ┗ 好きなファイル
    ┃
    ┗ public(git管理される)
```


# どんな感じで使うの

jupyterにログインしたら

    - publicフォルダ
    - privateフォルダ

の２つディレクトリがあるので
基本的には

    1. publicフォルダに適当なディレクトリを作ってメモを作る
    2. メモできたら適当なタイミングでgit commitしてgithubにあげる
    3. 他の人のメモが気になってきたらpullしてくる

で運用します.

publicフォルダはgit管理しないのでメモに残すほどでもなかったり、
単純にプログラムの挙動を確認する時に使って下さい.


# 初期設定

コマンド叩く前にdocker-compose動く環境を整える
```
$ cd tool-jupyter
$ cp .env.example .env
$ # jupyterのpassword変えたければ.env編集しましょう
$ docker-compose build
$ docker-compose up -d
```

そのあとはwebブラウザで`localhost:8888`にアクセスできるはず


# 気になりそうなところ

## jupyterって他のメモツールと何がちがうの

jupyter notebookは対話式のコンソールのようになっているので
他のツールと違って

    - プログラムを実行しながらメモできる
    - プログラムの実行結果が残る
    
ので今までだと試行錯誤の結果、間にどういったアプローチがあったかわからない
ってことが少なくなります。
機械学習だと基本的には殆どが成果物として残らないため、
途中の経過で使用したプログラムや知見をここに残せるのではないかと思ってます。

## ディレクトリどう切ればいいの

いま全く決まってないのでみんなで相談しましょう

## jupyterに使いたいlibraryないんだけど

dockerfileに
```
RUN pip install -U <使いたいlibrary>
```
ってかいて

```
$ cd tool-jupyter
$ docker-compose build
$ docker-compose up -d
```

ってやればinstallできるので動くと思います.

うまく動かんとかpython以外の何かをinstallしたくなったら

```
$ # 今動いてるjupyterの環境に入ってみる
$ docker-compose exec jupyter bash
$ # jupyterのimageから一時的にコンテナを立ててそこにインストールしてみる
$ docker run --rm -it jupyter/datascience-notebook bash
```

とかして試してからdockerfile書いてみて下さい.

できればそのlibrary他の人も使いたいはずなのでgithubにプルリクエスト送ってくれると嬉しいです.
