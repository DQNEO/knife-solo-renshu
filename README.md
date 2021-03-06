# knife soloの練習プロジェクト

## 公式サイト
* レポジトリ
https://github.com/matschaffer/knife-solo
* 公式マニュアル
https://github.com/matschaffer/knife-solo/blob/master/README.rdoc

# knife soloの使い方

## 準備編

* 事前にリモートホストにパスワードなしでsudoできるユーザを作っておく
* ssh user@remotehostで公開鍵認証ログインできるようにしておく

## help

忘れたらいつでもこれを見よ
```
knife solo cook  --help
```

## sshオプション
-i,-pなどはsshオプションとして働く
```
knife solo cook -i ~/.ssh/myprivatekey -p 2222 user@host
```
sshコマンドと同じく、~/.ssh/configにデフォルト値を設定することができる。

## prepare

リモートホストにChefをインストールしてくれる。

(逆に言うと、リモートホストに手動でChefDKを入れればいいだけなので、prepareは別に使う必要ない)

```shell
remote=ec2-xx-xx-xx-xx.ap-northeast-1.compute.amazonaws.com

# remoteにChefクライアントがインストールされる
# nodes/${remote}.jsonが生成される
knife solo prepare root@$remote
```


## cook

レシピがリモートで実行される

### デフォルトでは、nodes/${remote}.jsonが使われる。

```
# そのままだとrun-listが空なので何も起こらないので
# "Converging 0 resources"となる
knife solo cook root@$remote
```

### -N,--node-nameで任意のjsonファイルを指定できる
```
# nodes/hoge.jsonを指定
knife solo cook --node-name hoge root@$remote
```

#### -o でrun_listを指定できる
```
# 下記３つはどれも同じ意味
knife solo cook -o greet root@$remote
knife solo cook -o greet::default root@$remote
knife solo cook -o recipe[greet::default] root@$remote

# roleも指定できる
knife solo cook -o role[greetall] root@$remote
# カンマ区切りで複数指定できる
knife solo cook -o role[foo],role[bar] root@$remote
# zshの展開がうまく行かないときはこう
knife solo cook -o 'role\[foo\]','role\[bar\]' root@$remote


# カンマ区切りで複数指定できる
knife solo cook -o greet::default,greet::morning root@$remote
```
