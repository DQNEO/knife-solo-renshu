# knife soloの練習プロジェクト

## knife soloの使い方
```shell
remote=ec2-xx-xx-xx-xx.ap-northeast-1.compute.amazonaws.com

# remoteにChefクライアントがインストールされる
knife solo prepare root@$remote

# Chef-Soloがリモートで実行されるが、
# run-listが空なので何も起こらない
# "Converging 0 resources"となる
knife solo cook root@$remote

# -o でrun_listを指定できる
knife solo cook -o berkshelf-minimum root@$remote
```
