---
title: "CDエクストラを焼いてみよう"
---

このページでは、CDエクストラを自分で焼く方法を解説する。同人音楽活動をやっている人は、是非ともご一読願いたい。

# 注意
CD-Rの容量は650もしくは700MB。音楽に変換するとそれぞれ74分42秒、79分58秒だ。だがパソコン向けデータを収録する関係上、音楽の収録時間はそれより短くなる事に留意されたい。

----

# 準備
まずは「cdrkit」もしくは「cdrtools」をインストールしよう。Linux/GNU/XやMacOSを使っている場合は、コマンドでパッケージをインストールできる。Windowsでは「Cygwin」をインストールし、そこにcdrkitをインストールすると良い。

## Debian系
```bash
sudo apt install cdrkit
```

## Fedora系
```bash
sudo dnf install cdrkit
```

## Slackware (slackpkgを使用)
```bash
sudo slackpkg install cdrkit
```

## Arch系
```bash
sudo pacman -S cdrtools
```

## Mac (Homebrewを使用)
```bash
brew install cdrtools
```

## Windows (APT-Cyg)を使用
```bash
apt-cyg install cdrecord mkisofs
```
----

# 音楽セッションを焼く
まずはデバイス番号を確認だ。
```bash
sudo cdrecord -scanbus
```

するとこのような実行結果が表示される(これは一例)
```bash
scsibus0:
        0,0,0     0) 'BUFFALO ' 'Optical Drive   ' '2.00' Removable CD-ROM
        0,1,0     1) *
        0,2,0     2) *
        0,3,0     3) *
        0,4,0     4) *
        0,5,0     5) *
        0,6,0     6) *
        0,7,0     7) *
```

ここでは「0,0,0」が光学ドライブとして、話を進める。

次に音楽セッションを焼いてみよう。収録曲分のWAVデータを用意して(ここではtrack01〜05とする)、このコマンドを実行しよう。

```bash
cdrecord gracetime=5 dev=0,0,0 speed=1 -dao -nocopy -pad \
 /path/to/track01.wav \
 /path/to/track02.wav \
 /path/to/track03.wav \
 /path/to/track04.wav \
 /path/to/track05.wav
```

オプションの意味は次の通り。

- 「gracetime=5」…焼く前に5秒待機する。この時間内に実行を停止できる。
- 「dev=0,0,0」…デバイス番号は「0,0,0」。
- 「speed=1」…1倍速で焼く。
- 「-dao」…ディスク・アット・ワンスで焼く。これをするとCDプレイヤーとの互換性が高まる。
- 「-nocopy」…SCMS対応機器でのコピーガードを「コピーワンス」にする。
- 「-pad」…オーディオトラックを2352byteの倍数になるようパッドする。

「/path/to/track##.wav」はトラックへのパスだ。

WAVデータは必ず標本化(サンプリング)周波数44.1kHz、量子化ビット数16bitで生成する事。

それと「-nocopy」を「-copy」に置き換えると無制限コピー、「-scms」に置き換えるとコピー禁止(SCMSの制限だからCCCDとは無関係)にできる。ただこのパソコンが普及した時代に、SCMSはあまり意味を成さないので、無制限コピーでもまあ問題ないだろう。現にNMIから発売されるタイトルは無制限コピーで販売しているから。

----

# エクストラセッションの準備

エクストラセッションのためのISO仮想ディスクを作ろう。

```bash
mkisofs -graft-points -joliet -rational-rock -udf -volid VOLUMEID \
 -path-list /path/to/pathlist.txt -cdrecord-params 0,47381 -output /path/to/image.iso
```

オプションの意味は次の通り。
- 「-graft-points」…ファイル名に接ぎ木(グラフト)ポイントを使用できるようにする。
- 「-joliet」…Joliet(マイクロソフトによるISO 9660の拡張)を有効化する。
- 「-rational-rock」…合理化されたRock Ridge(ロック・リッジ、IEEEによるISO 9660の拡張)のディレクトリ情報を作成する。
- 「-udf」…ユニバーサル・ディスク・フォーマット(UDF)を生成する。
- 「-volid VOLUMEID」…ボリュームラベルを「VOLUMEID」にする。最大11字で、任意の名前で良い。
- 「-path-list /path/to/pathlist.txt」…ファイルパス一覧を指定する。「/path/to/pathlist.txt」はトラックへのパスだ。
- 「-cdrecord-params 0,47381」…「cdrecord」のマジック・パラメーターを「0,47381」に指定する。
- 「-output /path/to/image.iso」…ISOの出力先を指定する。「/path/to/image.iso」はISOの保存先のパスだ。

ファイルパス一覧はこのように書く。イコールより後は必ず絶対パスで記録する。イコールより前はISOやCD上でのファイル名だが、可能な限りは日本語などの2バイト文字を使うのはよした方が良い。

```
dir1/hoge.flac=/path/to/hoge.flac
dir1/fuga.flac=/path/to/hoge.flac
dir2/foo.mp4=/path/to/foo.mp4
dir2/bar.mp4=/path/to/bar.mp4
readme.txt=/path/to/readme.txt
```

----

# エクストラセッションを焼く
ISOができたので、CD-Rに焼いてみよう。

```bash
cdrecord gracetime=5 dev=0,0,0 -tao /path/to/image.iso
```

「gracetime=5」と「dev=0,0,0」は、先程と同じだ。「-tao」はトラック・アット・ワンス(TAO)で焼く。

----

# ディスクの検査
ディスクは焼けたが、作業はまだ終わらない。最後にするべき事は、CDプレイヤーでの再生とパソコンでのデータ読み取りだ。

----

# 完成
おめでとう、そしてお疲れ様。

完成したディスクはbin+cueで吸い出し、手焼きCD-Rのマスターにするのも良いし、業者に提出してコピーやプレスのマスターにしてもらうのも良い。ただ業者によってはマルチセッションに対応していないので、その辺りの注意は必要だ。

