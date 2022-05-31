#  Issac sim マニュアル
<div style="text-align: right;">
中部大学 工学部 ロボット理工学科　村田 竜輔
</div>
<br>
<br>


#  Issac simとは
NVIDIA Omniverse Issac sim は、NVIDIAのロボットシミュレーションツールキットである。

#  インストールガイド
##  動作環境
|        | 最低スペック                         | 推奨スペック                         | ハイエンドスペック                                         | 
| ------ | ------------------------------------ | ------------------------------------ | ---------------------------------------------------------- | 
| OS     | Ubuntu 18.04 / 20.04                 | Ubuntu 18.04 / 20.04                 | Ubuntu 18.04 / 20.04                                       | 
| CPU    | Intel Core i7 (第7世代)　AMD Ryzen 5 | Intel Core i7 (第9世代)　AMD Ryzen 7 | Intel Core i9  Xシリーズ以降、AMD Ryzen 9 Threadripper以降 | 
| コア数 | 4                                    | 8                                    | 16                                                         | 
| RAM    | 32GB                                 | 64GB                                 | 64GB                                                       | 
| ROM    | 50GB SSD                             | 500GB SSD                            | 1TB NVMe SSD                                               | 
| GPU    | GeForce RTX 2070                     | GeForce RTX 3080                     | RTX A6000                                                  | 
| VRAM   | 8GB                                  | 10GB                                 | 48GB                                                       | 
<br>
##  ドライバ
IsaacSimの現在推奨されているドライバーバージョンは470.57.02以降である。\
NVIDIA GPUドライバーの最新の長期サポートバージョンを./runインストーラーでインストールするのがおすすめ。\
<br>

###  ドライバのインストール方法
1.  コマンドを実行。
```
$  ubuntu-drivers devices
```
2.  ドライバの一覧が表示されるので、OSが推奨するバージョン(recommended)を確認する。
```
base > haru > Ryzen3700X4 > ~ > $  ubuntu-drivers devices
== /sys/devices/pci0000:00/0000:00:03.1/0000:0d:00.0 ==
modalias : pci:v000010DEd00001E84sv0000107Dsd00002784bc03sc00i00
vendor   : NVIDIA Corporation
model    : TU104 [GeForce RTX 2070 SUPER]
driver   : nvidia-driver-470 - third-party non-free
driver   : nvidia-driver-470-server - distro non-free
driver   : nvidia-driver-510 - third-party non-free
driver   : nvidia-driver-465 - third-party non-free
driver   : nvidia-driver-455 - third-party non-free
driver   : nvidia-driver-460 - third-party non-free
driver   : nvidia-driver-510-server - distro non-free
driver   : nvidia-driver-450-server - distro non-free
driver   : nvidia-driver-515 - third-party non-free recommended
driver   : nvidia-driver-450 - third-party non-free
driver   : nvidia-driver-495 - third-party non-free
driver   : xserver-xorg-video-nouveau - distro free builtin
```
3.  推奨バージョンで問題がない場合は次のコマンドを実行。
```
$ sudo ubuntu-drivers autoinstall
```

バージョンを指定してインストールする場合はXXXをバージョンに置き換えて次のコマンドを実行。
```
sudo apt install nvidia-driver-XXX
```
4.  インストールが完了したら、再起動をする。
```
$ reboot
```
5.  ログインしたら、以下のコマンドでGPUのステータスを確認する。
```
$ nvidia-smi
```
