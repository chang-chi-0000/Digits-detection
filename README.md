# Digits-detection

# NCTU hw2
Before using HW3 dataset, first need to turn annotation into VOC format. The file comes from https://github.com/penny4860/svhn-voc-annotation-format

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
