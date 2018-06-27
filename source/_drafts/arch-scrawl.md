---
title: ArchLinuxの備忘録
id: 79
categories:
  - 備忘録
tags:
---

なんか備忘を適当に殴り書き
<!--more-->

### アクセス制限関連

特にWordpressや、HTTPサーバーのログを見ているとまぁ色々しようと頑張っているログが結構見受けられるんですね....(特に最近ひどい)

というわけでブロックしたり色々します。
ここでは"GeoIP"を使ったWeb(Apache)での云々

pacman -Sy
pacman -S geoip
pacaur -S apache-module_geoip2

### 固定IPについて    *1/31統合移行

&nbsp;

Hyper-VにArch入れて遊んでる。

netctlを使う

exampleから持ってきて任意設定
有効にするも、固定IPでなかったり、IPが振り当てられてなかったり

ステータスを見ると既にほかで使われてるよ的なエラー
自動振り当て(dhcpcd)やらをnetctl-ipplugdやらを止めるもうまくいかず....
一つづつ丁寧に止めて無効処理をちゃんとして無事動作。

&nbsp;

### Google-Drive-Ocamlfuse

&nbsp;

google-ocaml絡み

pacaur,fuse系入れておく

linux-headers入れて、[exfat-dkms-git](https://aur.archlinux.org/packages/exfat-dkms-git/)いれておく

g-dri-ocamlぶっ込む時に記述ミスってるから、書き換えるかファイルがないよって言うとこに該当ファイルをコピーしておく

    Error: Cannot find file /usr/lib/ocaml/camlidl/com.cmxa
     /usr/lib/ocaml/com.* &gt;  /usr/lib/ocaml/camlidl/com.*

まぁその後、modprobe fuseでコケるので
<pre class="r">[linux-lts-headers](https://www.archlinux.org/packages/core/i686/linux-lts-headers/) [linux-headers](https://www.archlinux.org/packages/core/x86_64/linux-headers/)</pre>
ltsか否かどちらかぶっ込む（どちらでも

あと、どのユーザでもアクセスできるようにするの/etc/fuse.confの
<pre>user_allow_other</pre>
をコメントアウト