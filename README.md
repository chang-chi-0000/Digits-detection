# Digits-detection

# HW2
Before using HW2 dataset, first need to turn annotation into VOC format. The file comes from https://github.com/penny4860/svhn-voc-annotation-format

Follow the step below, put data to the designated place and produce the format which model needs.(Since dataset size is too large need to  move by hand)

### Catogory
1.Performance
2.Achievement
3.Environment
4.Attention
5.Trickset
6.Download
7.Predict step
8.Train step
9.Reference

### Performance
| 訓練數據集 | 權值文件名稱 | 測試數據集 | 輸入圖片大小 | mAP 0.5:0.95 | mAP 0.5 |
| :-----: | :-----: | :------: | :------: | :------: | :-----: |
| VOC07+12+COCO | [yolo4_voc_weights.pth](https://github.com/bubbliiiing/yolov4-pytorch/releases/download/v1.0/yolo4_voc_weights.pth) | VOC-Test07 | 416x416 | - | 84.5 
| COCO-Train2017 | [yolo4_weights.pth](https://github.com/bubbliiiing/yolov4-pytorch/releases/download/v1.0/yolo4_weights.pth) | COCO-Val2017 | 416x416 | 42.8 | 66.0 

### Achievement
- [x] 主幹特徵提取網路：DarkNet53 => CSPDarkNet53
- [x] 特徵金字塔：SPP，PAN
- [x] 訓練用的技巧：Mosaic數據增強、Label Smoothing平滑、CIOU、學習率會餘弦衰減
- [x] activate函數：使用Mishactivate函數

### Environment
torch==1.2.0

### Attention
**注意不要使用中文標籤，文件中不要有空格！**   
**在訓練前需要在model_data下新建一個txt文件，文件中輸入需要的分類，在train.py中將classes_path指向該文件**

### Predict step
#### 1、使用預訓練權重
a、下載完後解壓縮，下載yolo4_weights.pth或者yolo4_voc_weights.pth，放入model_data

#### 2、使用自己訓練的權重
a、按照訓練步驟  
b、在yolo.py文件里面，在如下部分修改model_path和classes_path使其對應訓練好的文件；**model_path對應logs文件夾下面的權值文件，classes_path是model_path對應的分類**。  
```python
_defaults = {
    "model_path": 'model_data/yolo4_weights.pth',
    "anchors_path": 'model_data/yolo_anchors.txt',
    "classes_path": 'model_data/coco_classes.txt',
    "model_image_size" : (416, 416, 3),
    "confidence": 0.5,
    "cuda": True
}
```
c、執行predict.py
可能需要修改裡面的path使其指向包含test image的folder

### Train step
1、本文使用VOC格式进行训练。  
2、訓練前將標籤文件放在VOCdevkit文件夾下的VOC2007文件夾下的Annotation中。  (path 定義在voc2yolo4.py 跟 voc_annotation.py, 可以自行修改)  
3、訓練前將圖片文件放在VOCdevkit文件夾下的VOC2007文件夾下的JPEGImages中。  (path 定義在voc2yolo4.py 跟 voc_annotation.py, 可以自行修改)  
4、在訓練前利用voc2yolo4.py文件生成對應的txt。  
5、在執行根目錄下的voc_annotation.py，執行前需要將classes改成自己的classes。**注意不要使用中文標籤，文件中不要有空格！**  不必生成validation set, 這部分在train.py裡面有處理 
```python
classes = ["10", "1", "2" ....]
```
6、此時會生成對應的2007_train.txt，每一行對應其**圖片位置**及其**真實框的位置**。  
7、**在訓練前需要在model_data下新建一个txt文件，文件中输入需要的分類，在train.py中將classes_path指向該文件**，如下：   
```python
classes_path = 'model_data/new_classes.txt'    
```
model_data/new_classes.txt文件內容為：   
```python
10
1
2
3
...
...
```
8、執行train.py即可開始訓練。

### Reference
https://github.com/qqwweee/keras-yolo3/  
https://github.com/Cartucho/mAP  
https://github.com/Ma-Dan/keras-yolo4  
