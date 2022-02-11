総会議案書テンプレート
========================
これは，総会議案書のテンプレートリポジトリです．
コマンドを使って簡単に総会議案書リポジトリを生成することができます．

セットアップ手順
--------------------
セットアップですべきことは，次の7つです．

1. [リポジトリのセットアップ](#セットアップ手順)
2. [CIのセットアップ](#ciのセットアップ)
3. [テンプレートファイルとGitHubの課題の生成](#テンプレートファイルとissueの発行)
4. [会員に対するアクセス許可](#会員に対するアクセス許可)
5. [ブランチ保護ルールの作成](#ブランチ保護ルールの作成)
6. [SlackAppのセットアップ](#slackappのセットアップ)
7. [PRテスト](#prテスト)

リポジトリのセットアップ
---------------------
総会リポジトリ`soukai-{年度}-{回数}`を生成します．
1. `$ git clone git@github.com:ritscc/soukai-template.git`
でこのテンプレートをcloneしてください．（ここでフォークではないことに注意してください．）
2. 自身のターミナルで `soukai-template` フォルダがあるディレクトリに移動してください．
3. `$ cp -r soukai-template soukai-{年度}-{回数}` を実行してください． (e.g.) `cp -r soukai-template soukai-2019-2`
4. コピーした先のディレクトリに移動してください．
5. `$ git remote -v` を実行して `origin` が表示されていることを確認してください．
6. `$ git remote rm origin` を実行してください．
7. `$ git remote -v` を実行して何も表示されないことを確認してください．
8. [GitHub](https://github.com/ritscc) にアクセスして新しいリポジトリを作成してください．
名前は `soukai-{年度}-{回数}` としましょう．
9. `$ git remote add origin git@github.com:ritscc/soukai-{年度}-{回数}.git` を実行します．
(e.g.) `git remote add origin git@github.com:ritscc/soukai-2019-1.git`
10. `$ git remote -v` を実行して `origin` が表示されていることを確認してください．
11. `$ git push -u origin master` を実行してください．
12. GitHub上でリポジトリが更新されたことを確認します．
13. `$ mv .github.sample .github` を実行します．
14. `$ git add -A` `$ git commit -m 'setup github actions'` `$ git push` を順に実行します．

CIのセットアップ
-----------------------
CIとは，継続的インテグレーション(Continuous Integration)のことです．
設定を行うと，誤字や表記ゆれを，コミットのタイミングなどで，GitHubのPull requestsに，自動的に指摘してくれるようになります．

人手でやることを減らせるので，設定することを推奨します．
CIのセットアップ方法については，[README\_CI.md](docs/README_CI.md)に詳しく紹介しています．

テンプレートファイルとissueの発行
---------------------
LaTeXのテンプレートファイルとissueの発行を行います．
これらの作業は，担当者が編集するファイルの間違いを少なくし，
すべての担当部分をissueとして管理できるようにするために必要です．
これらの作業は[setup.py](setup/setup.py)を用いることで，簡単に設定することができます．

### setup.pyについて
年度などの初期設定をしたり，テンプレートファイルを生成するツールです．
soukai-templateからコピーした直後や，各局のブランチを作るときに使ってください．

Pythonの動作環境は以下の通りです．
- Python ver3.7
- 必須ライブラリ
    - jinja2
    - pyyaml

必須ライブラリは
```shell
$ pip install jinja2
$ pip install pyyaml
```
でインストールしてください．
詳しくは，[README\_setup.md](docs/README_setup.md)を見てください．

### 作業手順
カレントディレクトリが総会リポジトリになっていることを確認した上で，以下の手順を踏んでください．
1. 以下のコマンドを実行して，年度などの情報を設定する．
    ```shell
    $ cd setup
    $ python setup.py init
    ```
1. 生成されたassignee.ymlを書き換える．
1. 以下のコマンドを実行して，予めsubsection以降の文書を書くためのテンプレートファイルを生成する．
    ```shell
    $ python setup.py g
    ```
1. 以下のコマンドを実行して，GitHubのリポジトリにissueを発行する．
    ```shell
    $ python setup.py i
    ```

必ずこのツールを使って，予めsubsection以降の文書を書くためのファイルを生成して，
それを編集するように呼びかけてください．
これはコンフリクトを避けるためです．
タスクを作成する時に編集するべきファイルパスを明示しておくと混乱が減ると思われます．

会員に対するアクセス許可
-----------------------
会員が総会リポジトリにpushできるようにします．
1. 総会リポジトリの`Settings/Manage access`にアクセスします．
2. `Invite teams or people`からアクセスを許可していきます．Roleは以下のようにしてください．
    ```
    SystemManagement : Admin
    member20xx : Write
    ```

ブランチ保護ルールの作成
-----------------------
シス管局員以外がmasterブランチやdevelopブランチにpushしないよう，ブランチ保護ルールを作成します．

1. `$ git checkout -b develop`でdevelopブランチを作成し，`$ git push origin develop`でdevelopブランチをpushします．
2. 総会リポジトリの`Settings/Branches`で`Default branch`を`develop`に変更します(初期は`master`)．右側にある矢印のアイコンをクリックすることで変更できます．
3. `Branch protection rules`の隣の`Add rule`をクリックしてください．
4. `Branch name pattern`に`develop`と入力し，以下の項目にチェックを入れて下さい．わからなかったら過去の総会リポジトリを参照してください．
    * Require pull request reviews before merging
        ```   
        Require approving reviews : 3
        ```
    * Require status checks to pass before merging
        * Require branches to be up to date before merging
    * Restrict who can push to matching branches
        ```   
        People, teams or apps with push access : ritscc/systemmanagement
        ```
5. `Save changes`を押してください．
6. 4を`master`にも同様に行う．

SlackAppのセットアップ
-----------------------
Slack App(RCC soukai)のセットアップを行います．これは総会文書が

1. `release`する (developブランチからmasterブランチへのPRを作成する)
2. `pre-release`した後、`pre-release`を外す (リポジトリ右部の`Releases/Edit`で`This is a pre-release`のチェックを外す)

という手順を踏んだときに，Slackの`#soukai`にメッセージを投稿するアプリです．

### 作業手順
Slack Appをそのまま使う場合は以下の手順を踏んで下さい．[README_notify.md](docs/README_notify.md)を見て作り直してもいいですが，Scrapbox(ritscc-private)の`Slack App Webhook URL`の内容は必ず更新してください．

1. Webhook URLをScrapbox(ritscc-private)から取得します．`Slack App Webhook URL`というタイトルの記事に記載されています．

2. `Settings/Secrets/New repository secret`にWebhook URLを保存します．この時、Name属性は必ず`SLACK_WEBHOOK`にしてください。
    ```
    Name : SLACK_WEBHOOK
    Value : 取得したWebhook URL
    ```

3. (任意)投稿メッセージのカスタマイズをします．以上の作業では、下記のようなメッセージが投稿されることになります。

<img width="418" alt="スクリーンショット 2021-08-27 12 47 42" src="https://user-images.githubusercontent.com/50389029/131068908-1569e6a9-a0a0-4257-8617-fee94e7b6d92.png">

`Message`というテキストを変更したい場合は、`.github.sample/workflows/notify.yml`を下記のように変更してください。

```diff
    env:
+   SLACK_TITLE: "タイトルを記入するよ"
    SLACK_MESSAGE: ":tada: 総会文書がリリースされました"
    SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
```
詳しくは[action-slack-notify](https://github.com/rtCamp/action-slack-notify)を見てください．

PRテスト
-----------------------
最後にPRテストを行います．

1. 総会文書の作成手順にしたがって適当なファイルを編集します．
2. developへのPRを作成し，GitHub Actionsが適切に動作するか確認します．ビルドエラーが起きた場合は[README_builderror.md](./docs/README_builderror.md)を見てください．
3. 成功したらSlackで総会リポジトリ生成の旨を伝え，執筆作業を開始してもらいます．

総会リポジトリの設定は以上です．