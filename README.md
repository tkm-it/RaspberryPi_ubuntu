# ubuntu setup (for RaspberryPi) - TOP PAGE  

## セットアップする機器やOSについて  
+ RaspberryPi 4 model B
+ ubuntu 26.04 for RaspberryPi

## ① microSDカードにOSインストール  
※ ここはPCでの作業になります  
1. ubuntu公式サイトからRaspberryPi向けのubuntuイメージをダウンロード  
[ubuntu 公式サイト - ダウンロードページ ※2026-6-20時点](https://ubuntu.com/download/raspberry-pi)  
2. RaspberryPi imagerをダウンロード → インストール  
[RaspberryPi software ダウンロードページ ※2026-6-20時点](https://www.raspberrypi.com/software/)
3. RaspberryPi imager(ver.2.0.7)を使ってmicroSDカードにubuntuをセットアップ  
    1. microSDカードをスロットに差し込んでから RaspberryPi imager を起動する
    2. Device - 対象のRaspberryPiを選択
    3. OS - カスタムイメージを使うを選択し、1 でダウンロードしたubuntuイメージを選択
    4. ストレージ - スロットに挿入したmicroSDカードを選択

※ microSDカードはFAT32でフォーマットされる。FAT32は認識32GB上限だがRaspberryPi imagerを使うと32GBを超えて認識できるようになる。

## ② RaspberryPiで ubuntu を起動する  
※ ここからRaspberryPiでの作業になります
起動してデフォルトユーザーでログインする
初期アカウント情報は以下の通り (ubuntu 26.04 for RaspberryPi だけ？)  
ユーザー名 (login) : `ubuntu`  
パスワード (password) : `ubuntu`  
　→ ここでログインに成功すると、新しいパスワードの入力を求められるので、設定する

## ③ 必要な設定をセットアップしていく  
1. [Wi-Fiのセットアップ](Wi-Fi_Setup/step.md)  
2. [Bluetoothのセットアップ](Bluetooth_Setup/step.md)  

