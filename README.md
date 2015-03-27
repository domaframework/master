domaframework release controller
================================

リリース手順と開発バージョンの作成手順を示す。

注意点
-------------
doma と doma-gen の jar ファイルは Travis CI 上のビルドで Sonatype へ upload される。

その後、Sonatypeの管理画面の操作により Maven Central Repository へデプロイされるが、
doma や doma-gen に依存したプロジェクトは、Maven Centory Repository へのデプロイ完了後で
なければマージしてはいけない。

Travis CI 上でビルドされる際に Maven Repositoryからdoma または doma-gen の jar を取得するからである。

前提
-------------

この master プロジェクトと settings.gradle に記載されているすべてのサブプロジェクトを
git clone しておく。

リリース手順
-------------

build.gradle の `masterVersion` を変更する（SNAPSHOTを外す）。

次のタスクを実行する。

```sh
./gradlew gitPrepareRelease --stacktrace
```

次のタスクを実行する。

```sh
./gradlew build
```

リリースノートを更新する。

次のタスクを実行する。

```sh
./gradlew gitRelease --stacktrace
```

doma プロジェクトにてプルリクエストとマージを行う。
Tranvis CI から Sonatype へ jar がアップロードされたことを確認する。
Sonatype の管理画面から Maven Central Repository へデプロイする。
デプロイが完了するまで待つ。

doma-gen プロジェクトにてプルリクエストとマージを行う。
Tranvis CI から Sonatype へ jar がアップロードされたことを確認する。
Sonatype の管理画面から Maven Central Repository へデプロイする。
デプロイが完了するまで待つ。

残りのプロジェクトにてプルリクエストとマージを行う。

master プロジェクトを commit、push し、プルリクエストとマージを行う。

開発バージョンの作成手順
------------------------------

master プロジェクトを pull する。

build.gradle の `masterVersion` を変更する（バージョンを上げSNAPSHOTをつける）。

次のタスクを実行する。

```sh
./gradlew gitPrepareDev --stacktrace
```

次のタスクを実行する。

```sh
./gradlew build
```

次のタスクを実行する。

```sh
./gradlew gitDev --stacktrace
```

master プロジェクトを commit、push する。
