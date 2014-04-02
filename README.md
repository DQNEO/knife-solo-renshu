# knife soloの練習プロジェクト

## knife soloの使い方
```shell
remote=ec2-xx-xx-xx-xx.ap-northeast-1.compute.amazonaws.com

# remoteにChefクライアントがインストールされる
# nodes/${remote}.jsonが生成される
knife solo prepare root@$remote

# cook
# レシピがリモートで実行される
# デフォルトでは、nodes/${remote}.jsonが使われる。
# そのままだとrun-listが空なので何も起こらないので
# "Converging 0 resources"となる
knife solo cook root@$remote

# -N,--node-nameで任意のjsonファイルを指定できる
knife solo cook --node-name nodes/hoge.json root@$remote

# -o でrun_listを指定できる
# 下記３つはどれも同じ意味
knife solo cook -o greet root@$remote
knife solo cook -o greet::default root@$remote
knife solo cook -o recipe[greet::default] root@$remote

# カンマ区切りで複数指定できる
knife solo cook -o greet::default,greet::morning root@$remote

```
