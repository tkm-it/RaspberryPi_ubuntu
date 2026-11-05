# ubuntu setup (for RaspberryPi) - TOP > Python Setup  
  
[＜ TOP PAGE に戻る](../README.md)  
  
---  

Ubuntu は標準でPythonがインストールされています  
ですが、任意のPythonを使いたい場合に標準インストールのPythonを変えることで不具合が出る可能性もあったりするので、任意のPythonを使える `pyenv` をインストールして使うことにします  

< [参考情報： Ubuntuにpyenvをインストールする (Qiita) ](https://qiita.com/middle_aged_rookie_programmer/items/0eb574e92a52c923e7ec) >

## ① pyenvのインストール  
``` bash  
# Bash
git clone https://github.com/pyenv/pyenv.git ~/.pyenv
```    

## ② pyenv のパスを通す  
インストール直後はパスが通っていないため、パスを通してフルパスではなくコマンド名だけでコマンドが走るようにする  
ただし、環境によって少し違うので注意 (参考情報サイトのコマンドをまるまる貼り付けるので、WSLのやり方も入っています)  

``` Bash  
# Bash
# 一般のUbuntuの場合
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'command -v pyenv >/dev/null || export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc

# WSL2のUbuntuの場合
echo 'export PYENV_ROOT="$HOME/.pyenv"' >> ~/.bashrc
echo 'export PATH="$PYENV_ROOT/bin:$PATH"' >> ~/.bashrc
echo 'eval "$(pyenv init -)"' >> ~/.bashrc
```  

<strong>*※ ここで、後述(このページの一番最後)のトラブルシューティングをやっておくと、あとがスムーズです*</strong>  

## ③ セットアップ完了時の作業  

**(1) .bashrcを読み込ませる**  

``` Bash  
# Bash
source .bashrc
```  

**(2) pyenvのバージョンを表示させてみる**  
``` Bash  
# Bash
pyenv --version
```  
これでpyenvのバージョンが表示されたらpyenvのインストールは完了  
  
## ④ pyenvで選択可能なPythonをインストールする  
  
``` Bash  
# Bash

# インストールできるPythonバージョンを確認
pyenv install --list

# 希望のバージョンをインストール (以下は例)
pyenv install 3.9.13

# 対象バージョンがインストールできたことを確認
pyenv versions

# 対象バージョンがPythonコマンドで使われるようにするよう設定
pyenv global 3.9.13

# 設定確認
python --version
```  



## ※ トラブルシューティング  

### 1. pyenv install インストールエラー  
ubuntuではzlibがマストのようなので、インストールしておくこと  

``` Bash  
# Bash
sudo apt install -y \
    build-essential \
    zlib1g-dev \
    libssl-dev \
    libbz2-dev \
    libreadline-dev \
    libsqlite3-dev \
    libncurses-dev \
    xz-utils \
    tk-dev \
    libffi-dev \
    liblzma-dev \
    uuid-dev

# zlibインストール確認
> dpkg -s zlib1g-dev

# 表示されたテキスト内に 以下のテキストがあれば zlibインストール成功
  :  
  :  
Status: install ok installed  
  :  
  :  
```  

### 2. pyenv install ビルド失敗時のクリア処理  

``` Bash  
rm -rf /tmp/python-build.*
pyenv uninstall 3.15.2
pyenv install 3.15.2
```