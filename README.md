# ubuntu setup (for Raspberry Pi)  

## ① microSDカードにOSインストール  
※ ここはPCでの作業になります  
1. ubuntu公式サイトからRaspberry Pi向けのubuntuイメージをダウンロード  
[ubuntu 公式サイト - ダウンロードページ ※2026-6-20時点](https://ubuntu.com/download/raspberry-pi)  
2. Raspberry Pi imagerをダウンロード → インストール  
[Raspberry Pi software ダウンロードページ ※2026-6-20時点](https://www.raspberrypi.com/software/)
3. Raspberry Pi imager(ver.2.0.7)を使ってmicroSDカードにubuntuをセットアップ  
    1. microSDカードをスロットに差し込んでから Raspberry Pi imager を起動する
    2. Device - 対象のRaspberry Piを選択
    3. OS - カスタムイメージを使うを選択し、1 でダウンロードしたubuntuイメージを選択
    4. ストレージ - スロットに挿入したmicroSDカードを選択

※ microSDカードはFAT32でフォーマットされる。FAT32は認識32GB上限だがRaspberry Pi imagerを使うと32GBを超えて認識できるようになる。

## ② Raspberry Piで
