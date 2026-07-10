# ubuntu setup (for RaspberryPi) - TOP > Bluetooth Setup  
  
[＜ TOP PAGE に戻る](../README.md)  
  
---  

Ubuntu Serverには標準で `bluetoothctl` という強力な管理ツールが入っているので、これを使います

## ① Bluetoothツールの起動  
``` bash  
# Bash
sudo bluetoothctl
```  
実行すると、プロンプトの左側が `[bluetooth]#` に変わり、専用の入力待ち状態になります  

## ② コントローラーの準備  
管理モードの中で、以下のコマンドを順番に実行してラズパイ側のBluetooth機能を有効にします  
``` Bash  
# Bash
power on
agent on
default-agent
```  

## ③ ペアリングの実行  
1. Bluetooth機器側を「ペアリングモード（検出可能状態）」にします  
2. ラズパイ側でスキャンを開始します  
``` Bash  
# Bash [Bluetooth]
scan on
```  
3. 画面に近くのBluetoothデバイスが列挙されるので、その中からキーボードのMACアドレス（XX:XX:XX:XX:XX:XX のような形式）、またはデバイス名（Bluetooth Keyboard など）を探します
4. 目当のデバイスが表示されたらスキャンを止めます
``` Bash  
# Bash [Bluetooth]
scan off
```  
5. 見つかったMACアドレスに対してペアリングを行います  
``` Bash  
# Bash [Bluetooth]
pair XX:XX:XX:XX:XX:XX
```  
※ Bluetooth機器側でPIN入力を求められた場合は、指示の通り入力等を行います  
## ④ 次回以降自動接続の設定  
次回からラズパイの起動時に自動で繋がるように「信頼（Trust）」設定をしてから接続します  
``` Bash  
# Bash [Bluetooth]
trust XX:XX:XX:XX:XX:XX
connect XX:XX:XX:XX:XX:XX
```  
## ⑤ Bluetoothツールの終了  
ここまでの設定が完了したら、以下のコマンドでBluetoothツールから通常のモードに戻って終了になります  
``` Bash  
# Bash [Bluetooth]
quit
```  
