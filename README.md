# DockerでGUIアプリを実行する際のサンプル

## 実行手順

1. ビルド

    以下のコマンドを実行する。

    ```bash
    docker compose build
    ```

1. 実行

    - 実行時にユーザーを指定する場合


        ```bash
        docker compose run --rm --user $(id -u) app
        ```

    - 設定ファイルでユーザーを指定する場合

        1. 設定ファイル(.env)の作成

            example.envをコピーしてファイル名を.envに変える。
            .envにはdockerを実行するユーザーのUIDを記述する。
            以下は.envの例。

            ```
            # UIDは echo $UID で調べる。
            UID=1000
            ```


        1. 実行

            以下のコマンドを実行すると、GUIアプリが起動する。

            ```bash
            docker compose run --rm app
            ```

## 気になる点

docker-compose.yml内でホストの環境変数を取得できないときがある。
DISPLAY は取得できているのに、UID は取得できない。

仕様かもしれないが、docker-compose.ymlや.env内でbashによる設定値の取得ができない。
例えば ```user: $(id -u)``` や ```UID=$(id -u)``` のような記述がしたかった。


## 参考サイト

- [Dockerコンテナ上でGUIアプリを表示する（Linux）](https://zenn.dev/ysuito/articles/fdc4a49d83614a)
