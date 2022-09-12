#  Isaac sim マニュアル
<div style="text-align: right;">
中部大学 工学部 ロボット理工学科　村田 竜輔
</div>
<br>
<br>
日本語版が存在しなかったから一応作成したけど、ぶっちゃけ公式の英語版読んだ方がいい。Google翻訳かければ十分読みやすいし、動画付だし。


#  Isaac simとは
NVIDIA Omniverse Isaac sim は、NVIDIAのロボットシミュレーションツールキットである。

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
IsaacSimの現在推奨されているドライバーバージョンは470.57.02以降である。

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
```
base > haru > Ryzen3700X4 > ~ > $  nvidia-smi 
Wed Jun  1 00:38:24 2022       
+-----------------------------------------------------------------------------+
| NVIDIA-SMI 510.73.08    Driver Version: 510.73.08    CUDA Version: 11.6     |
|-------------------------------+----------------------+----------------------+
| GPU  Name        Persistence-M| Bus-Id        Disp.A | Volatile Uncorr. ECC |
| Fan  Temp  Perf  Pwr:Usage/Cap|         Memory-Usage | GPU-Util  Compute M. |
|                               |                      |               MIG M. |
|===============================+======================+======================|
|   0  NVIDIA GeForce ...  On   | 00000000:0D:00.0  On |                  N/A |
| 23%   37C    P8     7W / 215W |    255MiB /  8192MiB |      3%      Default |
|                               |                      |                  N/A |
+-------------------------------+----------------------+----------------------+
                                                                               
+-----------------------------------------------------------------------------+
| Processes:                                                                  |
|  GPU   GI   CI        PID   Type   Process name                  GPU Memory |
|        ID   ID                                                   Usage      |
|=============================================================================|
|    0   N/A  N/A      1006      G   /usr/lib/xorg/Xorg                 35MiB |
|    0   N/A  N/A      1687      G   /usr/lib/xorg/Xorg                130MiB |
|    0   N/A  N/A      1817      G   /usr/bin/gnome-shell               35MiB |
|    0   N/A  N/A     12789      G   ...672737063322708368,131072       28MiB |
|    0   N/A  N/A     13510      G   /usr/bin/anydesk                   12MiB |
+-----------------------------------------------------------------------------+
```

##  Isaac sim のインストール
1.  OmniverseLauncherをダウンロードする。https://www.nvidia.com/en-us/omniverse
2.  omniverse-launcher-linux.AppImageがダウンロードされるので、次のコマンドで実行権を与える。
```
$ sudo chmod +x omniverse-launcher-linux.AppImage
```
3.  実行してインストールする。
```
$ ./omniverse-launcher-linux.AppImage
```
4. キャッシュ・Nucleusをインストールする。


##  ROS/ROS2ブリッジの有効化

![Screenshot from 2022-06-01 01-28-08](https://user-images.githubusercontent.com/51279381/171226090-4776b5c4-8f3d-485f-bb95-cc13939a1d0b.png)
Window > Extensions をクリック。
![Screenshot from 2022-06-01 01-32-15](https://user-images.githubusercontent.com/51279381/171226699-113182a1-5c36-49cb-9a1c-4c97d61d282f.png)

![Screenshot from 2022-06-01 01-32-25](https://user-images.githubusercontent.com/51279381/171226708-025666e4-bd86-489e-8134-4d79538bfb3d.png)
Extensionsウィンドウの左上の検索欄にROSと入力する。\
ROS、ROS2どちらか使用する方のBridgeのみ有効化する。
![Screenshot from 2022-06-01 01-32-37](https://user-images.githubusercontent.com/51279381/171226715-5857cedf-5c9c-4d6f-9337-4bf4a90bc2f3.png)


#  ROSチュートリアル
##  2. Turtlebot3をインポートして動かす
##  2.1 実行環境
   -  Ubuntu20.04LTS
   -  ROS Noetic
   -  Turtlebot3 Waffle
##  2.2 前提条件
-  Isaac sim のインストール完了
-  ROS のインストール完了
-  Turtlebot3パッケージのビルド
-  roscoreの実行

##  2.3 目標
Isaac simでTurtle bot3をセットアップし、操作できるようにする
-  URDF Importerを用いて、Turtlebot3のモデルをインポート
-  ROS BridgeとROS OmniGraphノードの紹介
-  ROS Twist メッセージでロボットが動作するようにセットアップする


##  2.4  Turtlebot3 URDFのインポート
1.  Turtlebot3には.xacro形式のファイルが付属しているので、次のコマンドを実行してURDF形式に変換する。
多分、`turtlebot3/turtlebot3_description/urdf/turtlebot3_waffle.urdf.xacro`にあると思う。
```
$ rosrun xacro xacro -o <変換後ファイル名>.urdf <変換元ファイル名>.urdf.xacro
```

2.  Isaac sim のコンテンツタブ内のIsaac/Environments/Simple_Room/simple_room.usdを探す。
3.  新規ステージでsimple_room.usdをドラッグし、TransformプロパティのすべてのTranslateの数値をゼロにして原点に配置する。部屋の中のテーブルを見るには、少しズームインするといい。
4.  ウィンドウ上部のIsaac Utilsタブ内のWorkflows/URDF Importerを開く。
5.  URDF ImporterウィンドウのImport Optionセクションで既存の環境を維持するためにClean Stageのチェックを外し、Turtlebot3はモバイルロボットなのでベースリンクの修正をオフにし、ジョイントドライブタイプを速度に変更する。
6.  Importセクション内で、まずInput Fileでインポートする URDF ファイルを見つける。このImportボタンは、ファイルを選択した後にのみ有効になる。
7.  アセットが Omniverse Kit にインポートされると、アセットの .usd バージョンのコピーが自動的に保存される。.urdf ファイルが配置されているフォルダーとは異なる場合は、アセットを保存するフォルダーを出力ディレクトリに指定する。.urdfファイルに一致するフォルダー名が指定されたディレクトリに作成され、新しく作成されたフォルダー内に.usdファイルが作成されます。
8.  Stageタブ内の空のスペースをクリックしてステージ上のすべての選択を解除するか、ツリーで/Worldを選択する。そうしないと、Turtlebot をツリー上のランダム オブジェクトの子としてインポートしてしまう可能性がある。
9.  Importをクリックしてインポートする。
10.  Turtlebotがインポートされると、テーブル上に表示されるので床の真上に移動させる。
11.  Playを押すとTurtlebotが床の上に落ちる。

##  2.5  ロボットを操縦する
1.  