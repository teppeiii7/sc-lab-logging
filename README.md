# sc-lab-logging

## ansible

### local

* vagrantのセットアップ

```
gem install vagrant --no-ri --no-rdoc
vagrant box list

ssh vagrant@192.168.33.10
password vagrant

vagrant box add centos65 https://github.com/2creatives/vagrant-centos/releases/download/v6.4.2/centos64-x86_64-20140116.box
vagrant init centos65
```

* vagrantの起動/停止

```
# 起動
vagrant update

# 停止
vagrant halt
```

* ansibleの実行

```
vagrant provision
```

### dev

```
ansible-playbook site.yml -i inventories/hosts_dev -u [username]
```

### stg

```
ansible-playbook site.yml -i inventories/hosts_stg -u [username]
```

### prod

* 環境変数を追加
<br>※ [sc-maintenance]はssh/configで定義した踏み台サーバのhost名

```
export ANSIBLE_SSH_ARGS="-o ProxyCommand=\"ssh -W %h:%p sc-maintenance\" -o User=[username] -o StrictHostKeyChecking=no"
```

* 実行

```
ansible-playbook site.yml -i inventories/hosts_prod
```

* タグ指定して実行

```
ansible-playbook site.yml -i inventories/hosts_prod -t td-agent
```
