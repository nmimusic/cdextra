---
title: "CDエクストラを焼いてみよう"
---

このページでは、パソコンでCDエクストラを焼く方法を解説する。

# 必要なモノ
- パソコン(OSはLinux/Mac/BSDがお勧めだが、CygwinがあればWindowsでも動く)
- CD-R(700MB/79分のものがお勧め)
- CD-Rに対応する光学ドライブ
- 必要曲数のWAVデータ(44.1kHz/16bit)
- おまけデータ

以下はWAVとおまけデータのファイル例。作業用ディレクトリを作っておいた方が良いだろう。WAVは44.1kHz 16bitで書き出しておく必要がある。
```
track01.wav
track02.wav
flac/track01.flac
flac/track02.flac
dsf/track01.dsf
dsf/track02.dsf
```

# MS-Windowsの場合
初めに**cdrtfe**をインストールしよう。公式サイト([英語](https://cdrtfe.sourceforge.io/cdrtfe/index_en.html)/[独語](https://cdrtfe.sourceforge.io/cdrtfe/index_de.html)から、「DOWNLOAD」のページから「cdrtfe 1.5.9 Setup」を選んで、インストーラーをダウンロード。そして入手したインストーラーを起動し、画面の案内に従ってインストール作業を進めよう。

[cdrtfe-1.5.9.exe](http://sourceforge.net/projects/cdrtfe/files/cdrtfe/cdrtfe%201.5.9/cdrtfe-1.5.9.exe)

**Windowsでの手順は工事中です。もう少しお待ち下さい**

# Linux/GNU/X、BSDの場合
## K3bの導入と起動
初めに**K3b**をインストールしよう。K3bはDebian、Arch、Fedoraなどの主要なLGXや各種BSDディストロで、公式パッケージとしてインストールできる。次にインストールしたK3bを起動する。これで準備は完了だ。

なお、K3bはCD-DAやEXTRAの他、デジタルデータを記録するCD-ROM(XA含む)、MPEGビデオを記録するビデオCD(CD-DV/SV)などの作成もできる。

## ファイルの追加
「新しいプロジェクト」から「新しいミックスモードCDプロジェクト」すると画面下部にタブが開くので、「オーディオセクション」にWAV、「K3b data project」におまけデータを放り込む。CDテキストを埋め込みたい場合は、この時点で編集しておくのが良い。
{{< figure src="/cdextra/img/k3b-1.png" alt="audio" position="center">}}
{{< figure src="/cdextra/img/k3b-2.png" alt="audio" position="center">}}

## ディスクに焼く
「書き込む」ボタンを押すとウインドウが表示されるので、以下のように設定をしよう。

{{< figure src="/cdextra/img/k3b-3.png" alt="audio" position="center">}}

- 「書き込み」タブ
    - 書き込みモード…自動
- 「ファイルシステム」タブ
    - ボリューム名…任意の名称(アルファベット11文字くらいが妥当)
        - その他のフィールド…全て空でも良い
    - ファイルシステム…「カスタム」ウインドウを開き、「Rock Ridge 拡張を生成」「Joliet拡張を生成」「UDF構造を生成」にチェックを入れる
- 「その他」タブ
    - ミックスモードの種類…**「2番目のセッションにデータ(CD-Extra)」を選択。これをしないとエクストラ盤ではなくミックスモード盤が出来上がるので注意。**[よくある質問](/cdextra/faq)の「7. ミックスモードCDとはどう違うの？」も参照
    - データトラックモード …モード1、モード2のどちらかを指定

CDテキストを埋め込みたい場合は、「CD-Text」タブから「CD-Textを書き込む」にチェックを入れ、「タイトル」「演奏者」を入力する。

準備が終わったら「書き込む」ボタンを押してディスクに焼こう。出来上がったらCDプレイヤーやパソコンで再生してみよう。これで上手く動けば完成だ。

# ディスクを量産したい場合
自力で焼く場合は、ImgBurnの「イメージファイルをディスクから作成」を使えばbin+cue方式で吸い出せる。これをまたImgBurnで「イメージファイルをディスクに書き込み」機能で安全に焼くという方法がある。Linux/GNU/XやBSDでは、Wineを使ってバージョン2.4.2.0を動かすと良い。

大量に生産する場合は、作ったディスクを業者に納品して、プレス盤を作ってもらうなり、R盤に焼いてもらうなりするのも良いかも。

