# yolov4の環境設定・使い方
darknetのyolov4を使って歩行者用信号機を検出するモデルと信号の色を判別するモデルを作成した.  
ここではdockerを使い、yolov4で学習及び上記の学習したモデルのテストができる環境を紹介する.  

## 実行環境
以下の環境で使用した.  
|OS|Ubuntu 18.04|
|--|--|
|GPU|Geforce RTX 3060 Ti|

## 環境設定
### Dockerを使う
daisukekobayashiさんがDockerHubで公開している[image][]を使う.  
以下のコマンドでimageをpullする.  
```
docker pull daisukekobayashi/darknet:yolov4-gpu-cv-cc86-11.2.0-ubuntu18.04
```
[image]: https://hub.docker.com/r/daisukekobayashi/darknet/ "docker"  

### GitHubからダウンロード
```
git clone ...
```
また追加で、[google drive][]から画像データや学習済みモデルなどをダウンロードする.  
Google driveから**backup**と**obj**と**labels** を[yolo210811][]ディレクトリにダウンロードする.  

[google drive]: https://drive.google.com/drive/folders/1Ftsr-N1k9SR_-vhdVY7jeSRR7Ow1tybI?usp=sharing "drive" 
[yolo210811]: https://github.com/RikuUchida/PedestrianSignal_Detction_Yolov4/tree/main/yolo_210811 "cmdディレクトリ" 
## yolov4を実行
pullしてきたDocker imageを立ち上げる.  
```
docker run -gpus all --rm -it -v $PWD:/yolo_docker --name yolov4-gpu-11.2-18.04 daisukekobayashi/darknet:yolov4-gpu-cv-cc86-11.2.0-ubuntu18.04  
```
docker内のディレクトリを移動.  
```
cd yolo/darknet/yolo210811  
```

### yolov4のコマンド
学習済みモデルを使ってテストする.  
```
./darknet detector test data/obj.data cfg/yolo-obj.cfg backup/yolo-obj_last.weights
```
[yolo210811][]ディレクトリにある[exe_cmd.txt][]に実行コマンドの例がある.  

[exe_cmd.txt]: https://github.com/RikuUchida/PedestrianSignal_Detction_Yolov4/blob/main/yolo_210811/exe-cmd.txt "cmd.txt" 
