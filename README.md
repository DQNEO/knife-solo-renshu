
remote=ec2-54-249-183-211.ap-northeast-1.compute.amazonaws.com
knife solo prepare root@$remote

# Chef-Soloがリモートで実行されるが、
# run-listが空なので何も起こらない
# "Converging 0 resources"となる
knife solo cook root@$remote

# -o でrun_listを指定できる
knife solo cook -o berkshelf-minimum root@$remote
