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

**(1) Bluetooth機器側を「ペアリングモード（検出可能状態）」にします**  

**(2) ラズパイ側でスキャンを開始します**  
``` Bash  
# Bash [Bluetooth]
scan on
```  
  
**(3) 画面に近くのBluetoothデバイスが列挙されるので、その中からキーボードのMACアドレス（XX:XX:XX:XX:XX:XX のような形式）、またはデバイス名（Bluetooth Keyboard など）を探します**  

**(4) 見つかったMACアドレスに対してペアリングを行います**  
``` Bash  
# Bash [Bluetooth]
pair XX:XX:XX:XX:XX:XX
```  
※ Bluetooth機器側でPIN入力を求められた場合は、指示の通り入力等を行います  

---  

### 【 Tips (trouble shoot) 】  
  
ここで問題が発生する場合があります  
発生する確率が高いものは `Failed to Pair` (ペアリング失敗) です  
対処法の一例として以下のやり方があります  
+ <u>*戻って「② コントローラーの準備」をやり直し、確実性を上げるようにする*</u>  
``` Bash  
# Bash [Bluetooth]

# コントローラーの再起動 ( OFF => ON )
power off
power on

# エージェント(認証)の確実性を高める
agent KeyboardOnly  # agent on の代わり  ※この場合はキーボードの認証に絞り込む
default-agent
```  

+ <u>*ペアリングの時間切れ => 制限時間内にペアリングを完了させる*</u>  
Bluetooth機器側で、ペアリングモードの制限時間が設定されている場合があります  
`scan on` でBluetooth機器が見つかったら、速やかに `pair xx:xx:xx:xx:xx:xx` を打ち込み、急いで認証を済ませましょう

+ <u>*失敗したペアリングの設定をクリアしてからリトライする*</u>  
``` Bash  
# Bash [Bluetooth]

# 念のため、過去のペアリング履歴から削除
remove XX:XX:XX:XX:XX:XX

# キーボードの電源自体も一度切り、再度オンにしてペアリングモードにする

# 再挑戦
scan on
pair XX:XX:XX:XX:XX:XX
```  

+ <u>*接続を `pair` ではなく `connect` で行う</u>  
一部のBluetooth機器では、connectのほうがスムーズにいくケースもあるようです
``` Bash  
# Bash [Bluetooth]
connect xx:xx:xx:xx:xx:xx
```  

　比較的発生しやすい `Failed to pair` の対処法は以上のようになります  

---  

**(5) ペアリングが完了したらスキャンを止めます**  
``` Bash  
# Bash [Bluetooth]
scan off
```  
  
## ④ 次回以降 自動接続の設定  
次回からラズパイの起動時に自動で繋がるように、信頼（Trust）設定をしてから接続します  
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
