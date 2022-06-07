#  はじめに
最近、Isaac gymというツールの存在を知って使用する機会が増えたが、使う人が少ないのか記事自体も少なくて結構困ったので、自分の経験を元にいろいろまとめてみる。

#  実行環境
-  Ubuntu20.04LTS
-  Ryzen7 3700X
-  Geforce RTX2070SUPER
-  RAM 32GB
-  VRAM 8GB

#  Isaac gymとは
NVIDIAの強化学習用の物理シミュレーション環境である。
他のGym環境と違い、シミュレーションをGPUで実行し結果をCPUメモリにコピーすることなくGPUテンソルに保存することができる。また、これらの結果にアクセスするためのテンソルベースのAPIが提供されているため、強化学習の観測と報酬の計算をGPUでできる。これにより学習の高速化が図れる。
#  Isaac gymのインストール
##  必要動作環境
-  Ubuntu18.04 またはUbuntu20.04
-  Python3.6~3.8
-  NVIDIAドライバのバージョン:470以降
##  インストールの前に
Gymを設定すると依存関係であるnumpyやPyTorchなどのPythonパッケージが全て自動的にインストールされる。既存の環境を破壊しないためにも、新たに仮想環境を作成してインストールすることをおすすめする。以下を参考にするといい。
###  仮想環境の構築[anaconda]
1.  以下のコマンドで仮想環境を作成する。rlgpuの箇所は仮想環境名である。作成する際にPythonのバージョンを3.6~3.8の間で指定する。今回は3.7。
```
$  conda create -n rlgpu python==3.7
```
2.  仮想環境の有効化は次のコマンドを実行。
```
$  conda activate rlgpu
```
3.  仮想環境の無効化は次のコマンドを実行。
```
$  conda deactivate
````

##  インストール
isaacgym内のpythonディレクトリに移動し、依存関係のパッケージを以下のコマンドでインストール。仮想環境にインストールする場合は実行前に仮想環境のアクティベートを行う。
```
$  pip install -e .
```
#  Isaac gym ベンチマーク環境のインストール
1.  https://github.com/NVIDIA-Omniverse/IsaacGymEnvs
このサイトからクローンする。次のコマンドを実行。
```
$  git clone https://github.com/NVIDIA-Omniverse/IsaacGymEnvs.git
```
2.  クローンが出来たら、/IsaaGymEnvs/にディレクトリ移動し、次のコマンドを実行しインストールする。
```
$  pip install -e .
```
#  Isaac gym ベンチマーク環境の実行
このパッケージには、予め環境やPPOのアルゴリズム等が実装されている。
実装されている環境は、
-  Allegro_hand
-  Ant
-  Anymal
-  AnymalTerrain
-  BallBalance
-  Cartpole
-  FrankaCabinet
-  Humanoid
-  HumanoidAMP
-  HumanoidAMPHands
-  Ingenuity
-  Quadcopter
-  ShadowHand
-  ShadowHandOpenAI_FF
-  ShadowHandOpenAI_LSTM
-  ShadowHandTest
-  Trifinger
である。
学習をする際は/IsaacGymEnvs/isaacgymenvs次のコマンドを実行。
hogehogeには上記の環境名を入力。
```
$  python3 train.py task=hogehoge
```
ヘッドレスで実行する場合は次のコマンドを実行する。
シミュレーションをGUI表示しないため、学習の実行速度を上げることができる。
```
$  python3 train.py task=hogehoge headless=True
```
学習中は/run/hogehoge/nnに定期的に学習モデルが保存される。途中で学習を停止させて、再度実行する場合は次のコマンドを実行する。hogehogeは環境名に置換。
```
$  python3 train.py task=hogehoge checkpoint=runs/hogehoge/nn/hogehoge.pth
```
学習済モデルの推論のみの実行は次のコマンドを実行。
```
$  python train.py task=hogehoge checkpoint=runs/hogehoge/nn/hogehoge.pth test=True
```
## 実行時のGif
![Peek 2022-06-07 16-02](https://user-images.githubusercontent.com/51279381/172317312-3f956105-30d4-4a21-860f-71d62829e6cb.gif)
![Peek 2022-06-07 16-04](https://user-images.githubusercontent.com/51279381/172317324-fe679e53-704b-4242-9cc3-d008e6c445ef.gif)

