2023年度第二回総会議案書
========================
これは，2023年度第二回総会議案書リポジトリです．

ビルドステータス
-----------------------
RCCの総会文章はGitHub Actionsを用いて，総会文書のビルドを自動化しています．

PDFを生成するには，ベースブランチを`master`か`main`に設定して，Pull Requestを作成してください．
生成されたPDFは，[リポジトリのリリースページ](https://github.com/ritscc/soukai-2023-2/releases)にアップロードされます．


文章表現について
-----------------------
文章表現について統一表記をここに示します．
なお，文章表現訂正一覧表は，[文章構成ツール【unagi】のルールCSVファイル](https://github.com/ritscc/unagi/blob/master/rules.csv)を確認してください．

* 口調：**である調**(だ調はダメ)

* 数字：固有名詞(例：2023年度第二回総会)，慣用句(三日月)，一つ・二つなどの数え上げ，一回生・二回生 以外は**半角アラビア数字**
* 西暦等：**半角アラビア数字**
* 日付：**○○○○年○月○日**(例1：2013年10月1日，例2：10月1日，2日，3日)
* 期間：**○か月(か はひらがな)**

* 句読点：**，．(それぞれ全角)**
* カンマ・ピリオドも全角でお願いします(本来半角でなければならいものを除く(例：ファイル名，URL))
* 括弧：**( )(それぞれ半角)**
* カギカッコ：**「」(『』や""は「」へ)**
* 英数字：**原則半角**

* RCC・当会・本会：**本会**
* 本局・当局：**本局**
* 会員・部員：**会員**
* 定例会議・例会：**定例会議**
* サークルルーム・部室：**サークルルーム**
* プロジェクト発表会・成果発表会：**プロジェクト発表会**
* 2022年度・昨年度・前年度：**2022年度**
* 2023年度・今年度：**2023年度**
* 2024年度・来年度・次年度：**2024年度**
* 前期・春学期：**春学期**
* 後期・秋学期：**秋学期**

* おこなう：**行う**(な抜き)
* ひきづき：**引き継ぎ**（引継ぎや引継ではない）

間違えやすい用語

* **エポック立命21**：エポックやエポック21は間違いです
* **夏期/冬期休暇** ： 季節の季ではなく，期間の期です

各種サービス名称

* **RCC Wiki**：会内Wikiシステムを指す場合は，RCC Wikiで統一してください．
* **Google系サービス**：全てサービス名はカタカナで記述してください．（例：Googleドライブ・Googleドキュメント・Googleフォーム）

省略系用語（省略記法は，最終版発行前に執行委員長・システム管理局が修正を行います）

* **KC3**：関西情報系学生団体交流会は「KC3」で記述してください．
* **LT**：ライトニングトークは「LT」で記述してください．


Gitでの作業について
-----------------------
総会文書は，Gitで管理されています．
ここでは，Gitを使った執筆作業を説明します．

コマンドがわかる人は，この通りに作業するといい感じになるでしょう．
SourceTree(GUIツール)を利用する方は，それっぽい説明を頑張って解読してください．

### 作業を始める前に
作業を始める前に，このリポジトリをクローン(clone)する必要があります．
言い換えれば，総会議案書とそれを管理するGitのデータを取得するということです．

* SSHでのクローン: `$ git clone git@github.com:ritscc/soukai-2023-2.git`
* HTTPSでのクローン: `$ git clone https://github.com/ritscc/soukai-2023-2.git`

SSHの設定していない方はHTTPSからクローンしてください．
SSHでクローンしておくと，コミット作業が楽です．
後からでも`$ git remote`を使って，変更できますので，設定しておくとよいでしょう．

### ブランチについて
基本的に，次の2本のブランチが存在しています．

- master/main : バージョンができ次第，ここにマージ(統合)されます．ここは普段更新されません．
- develop : 開発用ブランチです．ここに作業用ブランチをマージしていくことで執筆を進めます．

### 作業の流れ（ワークフロー）
1. 自分が行う作業を「Issue/イシュー（課題）」として作成します．既にイシューが登録されていれば，この作業は不要です．
   GitHubの「Issues」ページ<https://github.com/ritscc/soukai-2023-2/issues>の「New Isuue」ボタンを押して，イシューを作成します．
   タイトルや説明は，他の人が読んでもわかるように書いてください．
   担当者は担当する人に割り当てしてください．

2. 作業前に，`$ git pull`しておきます．こうすることで，作業の衝突(コンフリクト)を少なくさせられます．

3. 担当者は，developブランチを起点に，作業用ブランチ(branch)を作成します．
   `$ git checkout -b <branchname> develop`
   ブランチ名は重複しないように任意で構いません．
   ブランチ名にイシュー番号を含めておくとブランチを探しやすくなり，重複もしないのでオススメです．
   イシュー番号は，課題名の左下に`#<数字>`の形式で書かれています．

4. 編集します．
   編集方法は，下の「文書の執筆作業について」の章をお読みください．

5. キリの良い所で，ファイルを追加(add)してコミット(commit)します．
   `$ git add <filename>..`
   `$ git commit`
   コミット時は，作業内容がわかるように書いてください．
   また，コミットのどれかに`Reopen #<イシュー番号>`を含めるようにしてください．

6. 完成したらリポジトリにプッシュ(push)します．
   `$ git push origin <branchname>`
   __(注)__ なお，先ほど挙げたmasterとdevelopにはプッシュできません．権限の管理を行っています．

7. <https://github.com/ritscc/soukai-2023-2/pulls>からプルリクエスト(Pull request)を作成します．
   画面右上の方の「New pull request」のボタンから作成してください．
   __(注)__ タイトルは，課題番号を`Fix #<イシュー番号> : <作業内容>`という形式で記述してください．
   左（base)には`develop`のブランチを，右(compare)には，先ほど自分がプッシュ(push)したブランチをセットします．
   `Reviewers`に，局員や共同担当者を設定しておくと，プルリクエストを作成した旨が通知されますので，活用しましょう．
   ※ なお，プルリクエストは，自分のブランチをベースブランチにマージしたいという申請のことです．

8. あとはレビューされてください．みんなはレビューしてください．
   問題点があれば，プルリクエストのコメントを使って，問題点を指摘してください．
   ここで問題ないと判断したら__13__に飛んでください．

9. 指摘などがあり，変更の必要がある場合は，先ほどのブランチで，編集しなおします．

10. 編集できたら，__add，commit，push!!!!!!__

11. 自分が作成したプルリクエストのページから，修正した点をコメントにして残しておきましょう．

12. 8～11を繰り返してどんどん良くしていきます．

13. レビューして問題無いと判断した人は，プルリクエストページ内の`Files changed`を開き，
    `Review Changes`から，`Approve`を選択し，`Submit review`を送信しましょう．

14. いい感じだったら，執行委員長かシステム管理局長の判断でdevelopブランチにマージ(marge)されます．

なおマージされた後に，developブランチをプル(`$ git pull`)すると，更新されているのが確認できます．

```shell
$ git pull
$ git log
```
わからなければSlackの[#soukai](https://ritscc.slack.com/messages/soukai/)で相談してください．全員で共有しましょう．

文書の執筆作業について
-------------------

### 総会文書の書き方
執筆の全体的な流れをここに記載します．
Gitを使った作業の4までの作業を完了していることを前提としていますので，
まだ作業を行っていない方は作業を済ませてください．

1. 担当している箇所に対応するファイルを作成，あるいは開きます．
   基本的には，担当している「イシュー」のページに記載されているファイルを編集すればよいでしょう．
   記載がない場合やタスクがない場合は，「ディレクトリ構成について」の節を参考にしてファイルを配置してください．
2. 執筆します．
   章や節，リスト等の文章以外の文書の構成要素は，LaTeXコマンドを用いると良いでしょう．
   全てのtexファイルは，`\subsection*{}`から始めるようにしてください．
   また，`\writtenBy`コマンドを使って文責も記述してください．
3. 総会文書執筆では，担当箇所ごとにファイルを分割しています．
   分割されたファイルは，章のファイルや局別のファイルで自動的に取り込まれるようになっています．
   「ディレクトリの構成」の節を参考にして，編集するファイルを確認しましょう．

### LaTeXについて
総会文書は，LaTeX（ラテフ）を用いて執筆します．
LaTeXは，書籍や雑誌，レポート，論文などの執筆に広く使われている，フリーの組版システムです．
担当箇所ごとにファイルを分割して，1つの文書を構成することができるため，複数人での作業に適しています．

LaTeXの書き方については，各自ググってください．

### 文章中で利用できるコマンド一覧
左の表現を記述したい場合は，右のコマンドを記述することで表示させることができます．
`{}`は引数です．

* 会計局 `\kaikeiDepartment`
* 会計局長 `\kaikeiChief`
* 会計局員 `\kaikeiStaff`

* 研究推進局 `\kensuiDepartment`
* 研究推進局長 `\kensuiChief`
* 研究推進局員 `\kensuiStaff`

* 渉外局 `\syogaiDepartment`
* 渉外局長 `\syogaiChief`
* 渉外局員 `\syogaiStaff`

* システム管理局 `\systemDepartment`
* システム管理局長 `\systemChief`
* システム管理局員 `\systemStaff`

* 総務局 `\soumuDepartment`
* 総務局長 `\soumuChief`
* 総務局員 `\soumuStaff`

* 執行委員長 `\president`
* 副執行委員長 `\subPresident`

* 一回生 `\firstGrade`
* 二回生 `\secondGrade`
* 三回生 `\thirdGrade`
* 四回生 `\fourthGrade`

* 文責：x y z `\writtenBy{x}{y}{z}`

利用例：
```latex
\writtenBy{\president}{立命}{太郎}
```

実行結果：
`文責：執行委員長　立命 太郎`

### ディレクトリ構成について

```
├── README.md - このファイル
├── document.tex - 総会文章の設定ファイル
├── src/
│   ├── zenki.tex - 第一回(春学期用)総会文書用メインファイル
│   ├── kouki.tex - 第二回(秋学期用)総会文書用メインファイル
│   ├── soukatsu/ - 総括用ディレクトリ
│   │   ├── zentai.tex - 全体総括メインファイル（全体総括用フォルダの内容を\input{}）
│   │   ├── 1kai.tex - 1回生総括
│   │   ├── 2kai.tex - 2回生総括
│   │   ├── 3kai.tex - 3回生総括
│   │   ├── kaikei.tex - 会計局 総括用フォルダの内容を\input{}するファイル（自動生成）
│   │   ├── kensui.tex - 研究推進局 総括用フォルダの内容を\input{}するファイル（自動生成）
│   │   ├── syogai.tex - 渉外局 総括用フォルダの内容を\input{}するファイル（自動生成）
│   │   ├── soumu.tex  - 総務局 総括用フォルダの内容を\input{}するファイル（自動生成）
│   │   ├── system.tex - システム管理局 総括用フォルダの内容を\input{}するファイル（自動生成）
│   │   ├── zentai/ - 全体総括用フォルダ（局，回生別以外のファイルはここに配置）
│   │   ├── kaikei/ - 会計局 総括用フォルダ
│   │   ├── kensui/ - 研究推進局 総括用フォルダ
│   │   ├── syogai/ - 渉外局 総括用フォルダ
│   │   ├── soumu/  - 総務局 総括用フォルダ
│   │   └── system/ - システム管理局 総括用フォルダ
│   ├── houshin/ - 方針用ディレクトリ
│   │   ├── zentai.tex - 全体方針メインファイル（全体方針用フォルダの内容を\input{}）
│   │   ├── 1kai.tex - 1回生方針(春学期のみ)
│   │   ├── 2kai.tex - 2回生方針
│   │   ├── 3kai.tex - 3回生方針
│   │   ├── kaikei.tex - 会計局 方針用フォルダの内容を\input{}するファイル（自動生成）
│   │   ├── kensui.tex - 研究推進局 方針用フォルダの内容を\input{}するファイル（自動生成）
│   │   ├── syogai.tex - 渉外局 方針用フォルダの内容を\input{}するファイル（自動生成）
│   │   ├── soumu.tex  - 総務局 方針用フォルダの内容を\input{}するファイル（自動生成）
│   │   ├── system.tex - システム管理局 方針用フォルダの内容を\input{}するファイル（自動生成）
│   │   ├── zentai/ - 全体方針用フォルダ（局，回生別以外のファイルはここに配置）
│   │   ├── kaikei/ - 会計局 方針用フォルダ
│   │   ├── kensui/ - 研究推進局 方針用フォルダ
│   │   ├── syogai/ - 渉外局 方針用フォルダ
│   │   ├── soumu/  - 総務局 方針用フォルダ
│   │   └── system/ - システム管理局 方針用フォルダ
├── .github/ - GitHub Actionsに使用されるツール群
├── docs/ - 総会文書リポジトリをセットアップする人向けのドキュメント類
├── setup/ - セットアッププログラムフォルダ
├── template/ - 自動生成に使われるテンプレートファイル群
├── tools/ - テストに使われるツール群
└── assignee.yml - setup.pyで使用する担当者設定ファイル
```

総会文書のセットアップ
---------------------
リポジトリやファイルのセットアップ方法は，[README\_setup.md](docs/README_setup.md)をご覧ください．
自動ビルドのセットアップ方法は，[README\_CI.md](docs/README_CI.md)をご覧ください．