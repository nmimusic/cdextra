---
title: "CDエクストラを焼いてみよう"
---

このページでは、パソコンでCDエクストラを焼く方法を解説する。

# 必要なモノ
- パソコン(OSはLinux/Mac/BSDがお勧めだが、CygwinがあればWindowsでも動く)
- CD-R(700MB/79分のものがお勧め)
    - 練習の際は書き換えが利くCD-RWがお勧め
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
## cdrtfeの導入と起動
初めに**cdrtfe**をインストールしよう。公式サイト([英語](https://cdrtfe.sourceforge.io/cdrtfe/index_en.html)/[独語](https://cdrtfe.sourceforge.io/cdrtfe/index_de.html)から、「DOWNLOAD」のページから「cdrtfe 1.5.9 Setup」を選んで、インストーラーをダウンロード。そして入手したインストーラーを起動し、画面の案内に従ってインストール作業を進めよう。

[cdrtfe-1.5.9.exe](http://sourceforge.net/projects/cdrtfe/files/cdrtfe/cdrtfe%201.5.9/cdrtfe-1.5.9.exe)

標準言語がドイツ語だが、翻訳ファイルをインストール時に指定すると英語とか中国語とか日本語（！）とかも使える。言語設定はcdrtfeを起動後、「Extra」→「Language」から選べるようになっている。

なお、K3bはCD-DAやEXTRAの他、デジタルデータを記録するCD-ROM(XA含む)、MPEGビデオを記録するビデオCD(CD-DV 1.0/2.0)、スーパービデオCD(CD-SV)などの作成もできる。

## オーディオセッションを焼く
まず上のタブから「Audio CD」(オーディオCD)を選び、WAVファイルを放り込む。

{{< figure src="/cdextra/img/burn/cdrtfe-1.png" alt="audio" position="center">}}

次に「Options」(オプション)を押すと下のようなウインドウが表示されるので、以下のように設定する。

{{< figure src="/cdextra/img/burn/cdrtfe-2.png" alt="audio" position="center">}}

- CD…「Close CD」(CDをクローズする)、「Multisession (for CD+)」(マルチセッション(CD+用))にチェックを入れる
- Writing mode(書き込みモード)…「disc at once」(ディスク アット ワンス)を選ぶ。こうすると通常のCDプレイヤーでも再生できるようになる。
- コピー…どれでも良い。カーステレオで聴きたい場合は「One copy allowed」(1回のコピーを許可する)または「Unlimited Copies」(無制限コピー)を選ぶ。

CDテキストを埋め込みたい場合は、「Write CD text」(CDテキストを書き込む)にチェックを入れよう。

それから無音時間の調整も忘れずに。「Tracks」(トラック)ボタンを押すと次の画面が出るので、「Pause between tracks」(トラック間の一時停止)から設定しよう。標準は2秒だが、ノンストップCDを作る場合や予めマスターデータで無音を追加してある場合は「no pause」(一時停止しない)に設定する。この画面ではCDテキストの編集もできるので、埋め込む場合はここで一緒に設定してしまおう。

{{< figure src="/cdextra/img/burn/cdrtfe-3.png" alt="audio" position="center">}}

設定が終わったら「Start」(開始)ボタンを押す。チェックが通るとポップアップウインドウが表示されるので、「OK」を押して焼き始めよう。作業が終わるとログ欄に「Execution completed.」(作業が完了しました。)と表示される。

**ここで上部のメニューから「Project」(プロジェクト)→「Clear all」(すべてクリア)を押して、オーディオセッションの情報を削除しなければならない。こうしないと第2セッションがミックスモード仕様になってしまう。**

## エクストラセッションを焼く
さて次はお待ちかね(？)、エクストラトラックの焼き込みだ。まず「Data Disc」(データディスク)タブを開き、おまけファイルを放り込む。

{{< figure src="/cdextra/img/burn/cdrtfe-4.png" alt="audio" position="center">}}

次にディスクの設定をしよう。「Options」ボタンを押すと下のようなウインドウが表示されるので、以下のように設定する。
- Disc(ディスク)…「Multisession」(マルチセッション)と「Close disc (no further session)」(ディスクをクローズする(追加セッションなし))にチェックを入れる
- Writing mode(書き込みモード)…「track at once」(トラック アット ワンス)を選ぶ

{{< figure src="/cdextra/img/burn/cdrtfe-5.png" alt="audio" position="center">}}

それからファイルシステムの設定。これは「Filesystem」(ファイルシステム)からできる。お勧めはJoliet、UDF、Rock Ridgeの有効化だ。

{{< figure src="/cdextra/img/burn/cdrtfe-6.png" alt="audio" position="center">}}

そして準備ができたら「Start」(開始)を押す。次に表示されるポップアップはいずれも「OK」を押せば良い。作業が完了すると、例によってログ欄に「Execution completed.」(作業が完了しました。)と表示される。

出来上がったらCDプレイヤーやパソコンで再生してみよう。これで上手く動けば完成だ。

# Linux/GNU/X、BSDの場合
## K3bの導入と起動
初めに**K3b**をインストールしよう。K3bはDebian、Arch、Fedoraなどの主要なLGXや各種BSDディストロで、公式パッケージとしてインストールできる。次にインストールしたK3bを起動する。これで準備は完了だ。

なお、K3bはCD-DAやEXTRAの他、デジタルデータを記録するCD-ROM(XA含む)、MPEGビデオを記録するビデオCD(CD-DV 1.0/2.0)、スーパービデオCD(CD-SV)などの作成もできる。

## ファイルの追加
「新しいプロジェクト」から「新しいミックスモードCDプロジェクト」すると画面下部にタブが開くので、「オーディオセクション」(ここがオーディオセッションになる)にWAV、「K3b data project」(ここがエクストラセッションになる)におまけデータを放り込む。CDテキストを埋め込みたい場合は、この時点で編集しておくのが良い。

{{< figure src="/cdextra/img/burn/k3b-1.png" alt="audio" position="center">}}
{{< figure src="/cdextra/img/burn/k3b-2.png" alt="audio" position="center">}}

次に「オーディオセクション」で、各トラックの上で右クリックをし、「プロパティ」を押す。すると「オーディオトラックのプロパティ」という画面が開くので、「オプション」タブを開いて次のように設定しよう。
- コピーの許可…SCMSによるコピーガードをしない
- ポストギャップ…標準では2秒(00000:02:00)。ノンストップCDを作る場合や、予めマスターデータで無音を追加してある場合は0秒(00000:00:00)に設定する。最後のトラックでは設定しなくて良い。

{{< figure src="/cdextra/img/burn/k3b-3.png" alt="audio" position="center">}}

## ディスクに焼く
「書き込む」ボタンを押すとウインドウが表示されるので、以下のように設定をしよう。

{{< figure src="/cdextra/img/burn/k3b-4.png" alt="audio" position="center">}}

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
