継続的インテグレーション(CI)の手引き
=====================

概要
---------------------
RCCでは，総会文書のビルドをCIツールを用いて自動化しています．
ビルド自動化のメリットは，ビルドの手間を減らすことができるということに尽きるでしょう．

現在の設定では，ブランチへのファイル変更があった場合、すぐに文章校正とビルドテストを行っています．
ビルドに関しては，Dockerコンテナのイメージであるalpine上にLatex環境を組み込んだ環境で行い，
文章校正は，文章校正ツールである[unagi](https://gitlab.com/ritscc/soukai/unagi)を利用しています．

この文書では，GitHub Actionsを用いたCIの設定方法について解説します．

GitHub Actionsを用いたCI
---------------------
### GitHub Actionsとは
GitHub上のリポジトリやイシューに対するさまざまな操作をトリガーとしてあらかじめ定義しておいた処理を実行できる機能です．
過去に使用されていた，WerckerやCircleCIなどのCIサービスは連携設定が必要でしたが，
GitHub Actionsではそういった設定なしに，GitHubだけでCI機能を実現できるため，気軽に利用できます．

### 作業手順
ビルドの設定に必要な手順を最初から順に示します．

0. .github.sampleを.githubに名前を変更します．
[総会文章テンプレート](https://github.com/ritscc/soukai-template#readme)の手順でリポジトリを初期化した場合はすでに完了していると思われます．
1. GitHubのシス管アカウント(ritscc-master)でログインし，右上のアイコンをクリック．`Settings/Developer settings/Personal access tokens`にアクセスし，`Generate new token`からトークンを発行し，手元に控えてください．なお発行する際は
```
Note : 総会リポジトリ名
Expiration : No expiration
```
を設定し，`repo`，`workflow`にチェックを入れ，ページ下部の`Generate new token`をクリックしてください．
なおこのトークンは`setup.py`によりissueを発行する際にも使用します．

2. 今回使用する総会リポジトリの`Settings/Secrets`にアクセスし，`New repository secret`をクリックします．

```
Name : ACCESS_TOKEN
Value : 発行したトークン
```
を設定してください．

3. Completed!

カスタマイズ
---------------------

カスタマイズを行ってくれる人を募集しています．総会文書の執筆をよりよくするようなソリューションを待っています．

本リポジトリの.github.sample内には，実行する処理とその処理を実行する条件を定義したものが記述されています．
ここを変更することで，ビルドの動作やデプロイの方法を変更することが可能です．

GitHub Actionsの仕様については，[GitHub Actions について学ぶ](https://docs.github.com/ja/actions/learn-github-actions)を参照してください．

