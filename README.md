# Pacemaker+corosyncを使ったクラスター構成サーバ構築

## 概要
Pacemaker+corosyncを使ってクラスターを組むためのAnsibleのPlaybook。
Vagrantで２台のサーバを用意すれば、すぐにクラスターを実現できる。

Vagrantで立ち上げるサーバは以下のIPが前提で記載。
変更する場合はhostsファイルを変更する
- 192.168.33.20
- 192.168.33.21

## 使い方

### playbook実行
```
$ ansible-playbook -i hosts site.yml -u vagrant -k
```

### 起動と停止
pacemakerとcorosyncの両方が立ち上がっている必要がある。
開始・停止方法は以下を使って両方を同時に上げるのが推奨。
```
$ sudo initctl start pacemaker.combined
$ sudo initctl stop pacemaker.combined
```

個別に上げる際はcorosync→pacemakerの順で上げるといい
```
$ sudo service corosync start
$ sudo service pacemaker start
```

### ノード状態確認
```
$ sudo crm_mon -D1
```

## 参考
http://linux-ha.sourceforge.jp/wp/archives/4051
