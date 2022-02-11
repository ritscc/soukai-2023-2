# リリース時にSlackに通知するワークフロー

[notify.yml](../.github.sample/workflows/notify.yml)はGitHubのreleaseイベントをトリガーに、ビルドの成功を通知するワークフローです．

> [pre-releaseの場合は通知しないようにして、pre-releaseを後から外した時にactionが走ってくれると最高.](https://github.com/ritscc/soukai-template/issues/203)

とのことなので、

1. `release`する
2. `pre-release`した後、`pre-release`を外す

の時に発火するよう設定しています。

## セットアップ時に必要なこと

前提として、**通知先のチャンネル**と**通知するSlack App**が必要です。

Slackへの通知には[Incoming Webhook](https://slack.com/intl/ja-jp/help/articles/115005265063-Slack-%E3%81%A7%E3%81%AE-Incoming-Webhook-%E3%81%AE%E5%88%A9%E7%94%A8)を使用しており、通知先チャンネルのWebhook URLが必要なので一応説明しておきます。

### 1. Slack Appを作成

[Your apps](https://api.slack.com/apps)から作成できます。

### 2. Webhook URLを取得

Appを作成したら、`Add New Webhook to Workspace`から通知先チャンネルのWebhook URLを取得してください。

```
curl -X POST -H 'Content-type: application/json' --data '{"text":"Hello, World!"}' <取得したWebhook URL>
```

を実行すると、連絡先チャンネルに`Hello, World!`のメッセージが投稿されるはずです。

### 3. SecretsにWebhook URLを保存

作成した総会リポジトリの`Settings > Secrets > New repository secret`からWebhook URLを保存できます。この時、Name属性は必ず`SLACK_WEBHOOK`にしてください。

![](https://user-images.githubusercontent.com/50389029/131068750-7e315077-a5e3-478e-8f44-ac0a3fc64e57.png)

## 投稿メッセージのカスタマイズ

以上の作業を終えると、下記のようなメッセージが投稿されることになります。

<img width="418" alt="スクリーンショット 2021-08-27 12 47 42" src="https://user-images.githubusercontent.com/50389029/131068908-1569e6a9-a0a0-4257-8617-fee94e7b6d92.png">

`Message`というテキストを変更したい場合は、`.github.sample/workflows/notify.yml`を下記のように変更してください。

```diff
  env:
+   SLACK_TITLE: "タイトルを記入するよ"
    SLACK_MESSAGE: ":tada: 総会文書がリリースされました"
    SLACK_WEBHOOK: ${{ secrets.SLACK_WEBHOOK }}
```

詳しくは[action-slack-notify](https://github.com/rtCamp/action-slack-notify)