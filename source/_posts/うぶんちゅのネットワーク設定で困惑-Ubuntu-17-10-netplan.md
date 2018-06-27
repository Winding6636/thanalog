title: 'うぶんちゅのネットワーク設定で困惑 .:Ubuntu 17.10 netplan:.'
author: Winding
tags:
  - Linux
  - Ubuntu
  - Network
categories:
  - Linux
  - Ubuntu
date: 2018-03-24 12:50:00
---
### なにこれ
それが彼の最初に出た一言であった。
はい。ゲーム用鯖にｳﾌﾞﾝﾖを使おうと思い、どうせなら最新のをぶっ込んで久々にうぶんちゅを触ろうと思い入れたわけですが、まぁどうやら色々変わっているようですね。
<!--more-->
そしてセットアップをして初めに躓いたのがネットワーク設定。
いつもどおりのほほ～んと、networkからいじろうと思ったのですがふと検索すると'netplan'とかいう何だそのプランって名前が出てきたので読んで、なるほどわからん。なんでまた変えたコノヤローとか思いながら設定してたら始め詰んだので書き残す。(まえがき長い)

さんぷルー☆
```yaml
# This file describes the network interfaces available on your system
# For more information, see netplan(5).
network:
  version: 2
  renderer: networkd
  ethernets:
    eth0:
      dhcp4: yes
```
で、まずはじめに躓いたのは'インデント'
はい。僕はTABを主に使う派なのですが....
`" Invalid YAML at //etc/netplan/01-netcfg.yaml line 0 column 0: found character that cannot start any token "`
`" found character that cannot start any token while scanning for the next token "`
といったエラーが出ます。はい。
構成ファイルであるyamlがタブ使えないですわ。(ﾊｰ
というわけでスペースでしましょう！

自分はIPv6も使うので(実際使われるとは言っていない)設定するんですが、v6は[ : ]でそれぞれ区切る関係で[ ' ]で挟まないと
`Invalid YAML at //etc/netplan/01-netcfg.yaml line column : did not find expected key`
といったエラーがでます。(でも多分複数とかでないならいらない？ gateway6ではなくても良かった)

他にも、インターフェイス周りで何故かコケたりしたのですがそんなこんなを乗り越えて出来たのがコレ

```yaml
# This file describes the network interfaces available on your system
# For more information, see netplan(5).
network:
  version: 2
  renderer: networkd
  ethernets:
    ens192:
      dhcp4: no
      addresses: [10.0.0.25/24,':::::::/64']
      gateway4: 10.0.0.111
      nameservers:
       addresses: [':::::::',':::::::',0.0.0.0,8.8.8.8]
      dhcp6: no
      gateway6: ':::::::'
```
といった感じ
なんかあんまりexampleも豊富ではなさ気だったので？


いじょ！

*この記事は書きかけです。たぶんそのまま出してると思う。はい。

参考元
https://websiteforstudents.com/configuring-static-ips-ubuntu-17-10-servers/
http://manpages.ubuntu.com/manpages/artful/man5/netplan.5.html
https://kledgeb.blogspot.jp/2017/06/ubuntu-1710-23-netplan.html