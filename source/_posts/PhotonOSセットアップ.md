title: PhotonOSセットアップ
author: Winding
date: 2018-02-12 11:56:49
tags:
---
Docker環境を構築するのにPhotonOSを使う。

<!-- more -->
ロケールの変更
enからjpへ、しかし
```bash
Generating locales...
localename...cannot open locale definition file `localename': No such file or directory
```
と出る
tdnfでパッケを入れる	glibc-langとglibc-i18n(多分これだけで行ける)
```bash
tdnf install glibc-lang glibc-i18n
locale-gen.sh
```
```done```と出ればOK


参照
http://blog.kurokobo.com/archives/2433

<!--
Dockerのセッツアップ

Storage移行
systemdのdockerサービスに
ExecStart=~~dockerd --data-root=/ディレクトリ を入れる
-g等は多分廃止された（--data-rootを使うようにエラーが出る) -->