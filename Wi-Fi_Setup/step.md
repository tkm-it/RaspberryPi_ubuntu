# ubuntu setup (for RaspberryPi) - TOP > Wi-Fi Setup  
  
[＜ TOP PAGE に戻る](../README.md)  
  
---  

Ubuntu Serverでは、従来の `iwconfig` や `/etc/network/interfaces` ではなく、`Netplan` というツールを使ってネットワークを管理するのが標準です。コマンド一発で繋ぐというよりは、設定ファイルを1つ書き換える形になります。  

## ① 設定ファイルを探す  
以下のコマンドで、設定用のYAMLファイルの名前を確認  
``` Bash  
# Bash
ls /etc/netplan/
```  
（通常は `50-cloud-init.yaml` や `10-wader-network.yaml` のような名前のファイルが1つ入っています → 今回は `50-cloud-init.yaml` でした）  
  
## ② 設定ファイルを編集する  
管理者権限で設定用YAMLファイルを編集(vi/vim/nanoなど好きなエディタで)  
``` Bash  
# Bash
sudo nano /etc/netplan/50-cloud-init.yaml
```  
  
## ③ Wi-Fi情報を追記する
yamlファイルは、pythonと同様にインデントでネスト判定するので、ネスト階層とインデント数に留意して入力すること  
``` yaml  
# yaml file
network:
    ethernets:
        eth0:
            dhcp4: true
    wifis:
        wlan0:
            dhcp4: true
            access-points:
                "Wi-FiのSSID":
                    password: "Wi-Fiのパスワード"
    version: 2
```  

## ④ 設定を適用する  
以下のコマンドで設定を反映  
``` Bash  
# Bash
sudo netplan apply
```  
少し待ってエラーが出なければ、無事にWi-Fiに繋がっているはずです  
  
---  
## 【確認方法】  
以下のコマンドでIPアドレスが割り当てられれているか確認  
``` Bash  
# Bash
ip a s wlan0
```  
