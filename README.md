# PedestrianSignal_Detction_Yolov4

<img src="https://user-images.githubusercontent.com/54020567/166098008-34c12776-6c8f-4c4a-bd73-c380e916c4e0.gif" width="270px"><img src="https://user-images.githubusercontent.com/54020567/166098026-5a9876cc-25b8-4b7a-9479-1a843b66e479.gif" width="270px"><img src="https://user-images.githubusercontent.com/54020567/166098040-cc93a607-8b2c-4a3c-acee-a7cbde612948.gif" width="270px">  

# 概要
[AlexeyAB/darknet][]のyolov4を使用し, 歩行者用信号機を検出するモデルと信号の色を判別するモデルを作成した. 
本パッケージでは作成したモデルを使用することで信号の認識（歩行者用信号機, 信号の色）を行うことができる. 

## 実行環境
* Ubuntu 18.04 desktop
* AMD Ryzen7 3700X 8-Core Processor
* Geforce RTX 3060 Ti

# 使用方法

dockerを使用することでyolov4のための環境構築を行う. 
またyolov4にて学習及び上記の学習したモデルのテスト方法について紹介する.  

[AlexeyAB/darknet]: https://github.com/AlexeyAB/darknet "alexeyAB"

## 環境設定
### Dockerを使う
[daisukekobayashi](https://hub.docker.com/u/daisukekobayashi)がDockerHubで公開している[docker image(daisukekobayashi/darknet)][]を使う.  
以下のコマンドでimageをpullする. 
```
docker pull daisukekobayashi/darknet:yolov4-gpu-cv-cc86-11.2.0-ubuntu18.04
```
[docker image(daisukekobayashi/darknet)]: https://hub.docker.com/r/daisukekobayashi/darknet/ "docker"  

### GitHubからダウンロード
```
git clone https://github.com/RikuUchida/PedestrianSignal_Detction_Yolov4.git
```
また追加で, [google drive][]から画像データや学習済みモデルなどをダウンロードする.  
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
学習済みモデルを使って信号機検出を行う.  
#### 画像を入力とする場合：
```
./darknet detector test data/traffic.data cfg/traffic.cfg backup/traffic_detect.weights
```
モデルの読み込みなどが終わると以下の入力が出力される
```
Enter Image Path:
```
画像のPATHを入力すると下の画像のように出力される.  
![predictions](https://user-images.githubusercontent.com/54020567/166098516-37b1059d-dd9a-429f-a3a7-1b1eb4972d09.jpg)

#### 動画を入力とする場合：
```
./darknet detector demo data/traffic.data cfg/traffic.cfg backup/traffic_detect.weights MOVIE_PATH -out_filename SAVE_PATH
```
***MOVIE_PATH***には動画のPATHを入力し, ***SAVE_PATH***には出力される動画の保存場所を入力する.  
出力される動画の例:  
<img src="https://user-images.githubusercontent.com/54020567/166098008-34c12776-6c8f-4c4a-bd73-c380e916c4e0.gif" width="320px">
<img src="https://user-images.githubusercontent.com/54020567/166098026-5a9876cc-25b8-4b7a-9479-1a843b66e479.gif" width="320px">
<img src="https://user-images.githubusercontent.com/54020567/166098040-cc93a607-8b2c-4a3c-acee-a7cbde612948.gif" width="320px">  
[yolo210811][]ディレクトリにある[exe_cmd.txt][]にその他実行コマンドの例がある.  
  
***信号の色を判別する場合***は各コマンドの***trafficをcolourに置換***すると色判別のモデルが読み込まれる.  

[exe_cmd.txt]: https://github.com/RikuUchida/PedestrianSignal_Detction_Yolov4/blob/main/yolo_210811/exe-cmd.txt "cmd.txt" 
