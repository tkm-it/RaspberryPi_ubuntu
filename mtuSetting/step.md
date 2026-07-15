# ubuntu setup (for RaspberryPi) - TOP > MTU Setting (公衆Wi-Fi使用時に、データ最大送受信サイズを通信環境に合わせる方法)  
  
[＜ TOP PAGE に戻る](../README.md)  
  
---  
RaspberryPi で発生するかわからない現象で、  
WSL + ubuntu24.04 で発生したトラブルの解消手順になります  

## トラブルが発生する経緯  
公衆Wi-Fi(wi2eap)などは「WPA2-Enterprise (EAP)」という強固なセキュリティ（証明書やID/PWによる端末認証）を使って接続しています  
また、公衆Wi-Fiサービスは内部でVPN（トンネリング技術）や特殊なカプセル化（VLANなど）を使って通信を保護・カプセル化していることがほとんどです  

このカプセル化が行われると、1度に通せるデータの最大サイズ（MTU）が通常（1500）よりも小さくなります（例：1400前後）  

+ 小さいファイル（数百KB）：  
パケット数が少ないため、MTUのズレがあっても強引に届き、ダウンロードに成功します  
+ 大きいファイル（26MBのLLVMなど）：  
パケットが連続して大量に送られます。WSLが「1500バイトで送って！」と要求しているのに、Wi-Fi経路上が「いや、うちは1400バイトまでしか通せないから」とパケットを途中で破棄（ドロップ）してしまいます。結果としてデータの一部が壊れ、「届いたファイルのハッシュが計算と合わない（Hash Sum mismatch）」というエラーになります  
  
## 対処法：WSLのMTU値を「1300」に下げてみる
WSL2の仮想ネットワークアダプタのMTU設定を小さくして、au Wi-Fiの制限に合わせることで解決します  

1. Ubuntuのターミナルで、現在のネットワーク名（通常は eth0）を確認する  
``` Bash
ip link show

# 結果（例）
1: lo: <LOOPBACK,UP,LOWER_UP> mtu 65536 qdisc noqueue state UNKNOWN mode DEFAULT group default qlen 1000
    link/loopback 00:00:00:00:00:00 brd 00:00:00:00:00:00
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP> mtu 1500 qdisc mq state UP mode DEFAULT group default qlen 1000
    link/ether 00:15:5d:e4:90:90 brd ff:ff:ff:ff:ff:ff
```
2. MTU値を「1300」に一時的に下げる
``` Bash
sudo ip link set dev eth0 mtu 1300
```
3. この状態で再度アップデートを試す
``` Bash
sudo apt upgrade
```
などを試して、ErrではなくすべてGetできればOK  
それでも一部Errになるなら、さらにMTUを小さくする  

