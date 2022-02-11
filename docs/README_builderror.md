LaTeXのBuildに失敗したとき
=====================
2021年9月現在までで確認されている原因として
* [entrypoint.sh](/.github.sample/actions/latex/entrypoint.sh)に権限がない

というものがありました(一応これはDockerfileの変更により修正されたはずですが)．

entrypoint.shに権限がない
--------------------
 
 解決するには以下のコマンドを順に実行してください．
 ```
$ git checkout develop
$ git config core.filemode=true
$ chmod +x entrypoint.sh
$ git add entrypoint.sh
$ git commit(以下略)
$ git push origin develop
$ git config core.filemode=false
$ git checkout (テストのときに作ったブランチ)
$ git pull origin develop
 ```
以上のことをした後，もう一度テストをするとBuildに成功すると思います．