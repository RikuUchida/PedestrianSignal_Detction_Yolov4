# yolov4の環境設定・使い方
darknetのyolov4を使って歩行者用信号機を検出するモデルと信号の色を判別するモデルを作成した.  
ここではdockerを使い、yolov4で学習及び上記の学習したモデルのテストができる環境を紹介する.  

## 環境設定
### Dockerを使う
daisukekobayashiさんがDockerHubで公開しているimageを使う.  
以下のコマンドでimageをpullする.  
```
docker pull daisukekobayashi/darknet:yolov4-gpu-cv-cc86-11.2.0-ubuntu18.04
```

### GitHubからダウンロード
```
git clone ...
```
google driveから画像データや学習済みモデルなどをダウンロードする.  

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

yolo210811ディレクトリにある **exe-cmd.txt** に実行コマンドの例がある.  
