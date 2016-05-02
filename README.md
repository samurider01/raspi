# raspi

### Raspberry-Pi2の初期セットアップ

* Raspbian(OS)をダウンロードします。<br>
https://www.raspberrypi.org/downloads/raspbian/<br>
※ZIPファイルのダウンロードに約10分

* ダウンロードファイルを解凍して、imgファイルを取り出します。

* OSのimgファイルをmicro-SDに書き込むためのソフトウェア「win32diskimager」をインストールします。
http://sourceforge.net/projects/win32diskimager/

* win32diskimagerを使って、microSDにimgファイルを書き込み(write)します。<br>
※書き込み時間は約8分

* RaspberryPiにmicroSDとLANケーブル、USBケーブルを差し込んで起動します。

* Wifiの管理画面などから、RaspberryPiのIPを特定します。

* ターミナルソフト(Teraterm/Putty等)より、RaspberryPiにSSH接続します。<br>
IP:？<br>
Port:22<br>
id:pi<br>
pass:raspberry<br>

* 無線Lanの子機をRaspberry PiのUSBに差し込みます。

* lsusbと入力して、子機が表示されていることを確認します。
~~~
pi@raspberrypi:~ $ lsusb
Bus 001 Device 004: ID 0411:01a2 BUFFALO INC. (formerly MelCo., Inc.) WLI-UC-GNM Wireless LAN Adapter [Ralink RT8070]
Bus 001 Device 003: ID 0424:ec00 Standard Microsystems Corp. SMSC9512/9514 Fast Ethernet Adapter
Bus 001 Device 002: ID 0424:9514 Standard Microsystems Corp.
Bus 001 Device 001: ID 1d6b:0002 Linux Foundation 2.0 root hub
~~~

* Wifi設定ファイルに設定を追加します。
~~~
$ sudo vim /etc/wpa_supplicant/wpa_supplicant.conf
-------------------------------------
country=GB
ctrl_interface=DIR=/var/run/wpa_supplicant GROUP=netdev
update_config=1

↓↓ ここから追加 ↓↓
network={
   ssid="{無線ルータの親機のSSID}"
   proto=WPA2
   key_mgmt=WPA-PSK
   psk="{無線ルータの親機に設定されているパスワード}"
}
~~~

* RaspberryPiを再起動します。
~~~
$ sudo reboot
~~~

* 起動後、SSH接続して無線LAN子機のipを調べます
~~~
ifconfig
~~~

* 調べたIPを指定してターミナルよりSSH接続します。

* ディスクサイズを拡張します。
http://yamaryu0508.hatenablog.com/entry/2015/02/03/070000

* vimをインストールします
~~~
$ sudo apt-get install vim
~~~

#### 参考サイト
http://lchikaamazon.hatenablog.com/entry/2013/11/18/171637


### Node環境構築

* rootユーザに昇格します。
~~~
$ sudo su - 
~~~

* githubよりnvmをcloneします。
~~~
# git clone git://github.com/creationix/nvm.git ~/.nvm
~~~

* nvm.shを読み込みます。
~~~
# source ~/.nvm/nvm.sh
~~~

* 起動スクリプトにもnvm.shの読み込みを追加しておきます。
~~~
# vim ~/.bashrc
~~~

* Nodeのバージョンリストを表示します。
~~~
nvm ls-remote
→最新ばv6.0.0
~~~

* 最新のNodeをインストールします。
~~~
# nvm install 6.0.0
~~~

* 最新のNodeがインストールされたことを確認します。
~~~
# nvm ls
->       v6.0.0
         system
default -> 6.0.0 (-> v6.0.0)
node -> stable (-> v6.0.0) (default)
stable -> 6.0 (-> v6.0.0) (default)
iojs -> N/A (default)
~~~

* npmをインストールします。
~~~
# apt-get install npm
~~~
