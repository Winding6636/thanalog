title: お一人様AdventCalendar Act.1 -WSLデスクトップ環境編-
date: 2017-12-05 03:45:22
---
#### <div style="text-align: center;">何言ってんだこいつ</div> 
---
### 何始めんの？

こ↑こ↓は Advent Calendarしたいけどんーどうしようと悩んでとりあえず一人でやるだけやろうというお一人様アドベントカレンダー初日の記事です。
<!--more-->
公式やらqiitaとかにわざわざ立てるほどでもなかったり、どっかに入るのも気が引ける（自分の中で明確に決まっていない時)ということでれんしうも兼ねて、お一人で勝手にやってろなものです。テーマも多分ネタ切れてまちまちになると思います。とりあえず、毎日と言っても三日坊主になりそうなので週１から初めてXmasが近づくに連れ徐々に週１から増えていくという感じでやろうと思います。

###### <s> ヤバイネタ忘れた</s>
<!-- ここからが本当の勝負 -->
### ここからが本当の勝負

今回のテーマはズバリ、Windows Subsystem for Linux(WSL) ✕ Linux
wslとLinux Desktop

自分のWSL環境を今回はご紹介。
自分は以前、VMwareにあるシームレス機能を使ってWindowsとLinuxのハイブリッド環境みたいなものを作って作業等していた時期があるのですが、仮想マシンを動かす都合上、そのOS分＋少し余裕を持たせたメモリを消費するのでどちらかで重い(メモリ消費の多い)作業をする時に落としたりとかの手間が少しだけありました。(同時並行で作業したりする場合もあるので..

そんな時、Windows10でWSL(旧WindowsOnBash)がベータから始まり(FCUから正式)これでやったら楽じゃね？ということで構築しました。当初は完全なものではないので日本語や一部分で使えないところがあるのでその調整等が必要でしたがCUからは特段それも気にすることもないほどしっかりしてきてくれたのでそんな方法を書きます。

今回のイメージ
[画像]

構築環境
・Windows 10 Pro CU 1703
・X Window Server Client  VcXsrvなど 1.19.3.3
・WSL Ubuntu 16.04
・xorg 1:7.7+13ubuntu3
・MATE (mate-desktop-environment) 1.12.0+1
・uim-anthy 1:1.8.6-15
・fonts-vlgothic (特に必要ではない)
・お好みのWSL用ターミナル

WSLのインストールなどはこちらを参考に
[Windows 10でLinuxプログラムを利用可能にするWSL（Windows Subsystem for Linux）をインストールする](http://www.atmarkit.co.jp/ait/articles/1608/08/news039.html) (最近のもの)

WSLをインストールしたら、お好みのターミナルでbashを立ち上げて
apt update
apt install xorg mate uim uim-anthy fonts-vlgothic
＊今回使用するものは主にmate-panel,mate-settings-daemon,mate-applets,uimとなります。それ以外の余計なものを入れたくない方はこれらのパッケージのみ導入して下さい。

~/.bashrc をエディタで
export DISPLAY=localhost:0.0
export XIM=uim
export XMODIFIERS=@im=uim
export UIM_CANDWIN_PROG=uim-candwin-gtk
#export UIM_CANDWIN_PROG=uim-candwin-qt
export GTK_IM_MODULE=uim
export QT_IM_MODULE=uim

if [ $SHLVL -eq 1 ]; then
  uim-xim &
fi
を追記します。
~/.startx をエディタで
uim-xim&
uim-toolbar&
uim-fep&
mate-panel&
mate-settings-daemon&
を追記します。

