# yolov8_animeface
Anime Face Detection using YOLOv8

## Dataset
Dataset was made of 10 000 images manually annotated from safebooru. Split was train 70, val 20, test 10.

## Usage
One model is provided in the release page. Requirements are provided in the requirements.txt file.

All notebooks are provided to train, evaluate, and predict with the model. They're shipped with comments and notes to understand better yolov8's results.

To use the model, simply use

```python
from ultralytics import YOLO

yolov8_animeface = YOLO('yolov8_animeface.pt')
yolov8_animeface.predict('./images/', save=True, conf=0.3, iou=0.5)
```

Tweak conf and iou as you want.

## Performance

This model is based on yolov8x6. It has been trained on the said dataset for 300 epoch at 1280px*1280px. It took ~110 hours to train on a RTX A4000.

On my dataset, the model performs particularily well with the default parameters.

////// Insert good perf measurement here

```
Images  Instances    Box(P        R      mAP50     mAP50-95):
1002       1562      0.957      0.924      0.955      0.534
```

While it doesn't provide a huge mAP50-95, its predictions are always correct on the files I've tested. Confidence could be higher, but the model is very precise.

////// Insert demo here

## Comparison with an existing model

While we can argue about the comparison between two models from different generations, I believe it is interesting to compare this model with [zymk9's model based on yolov5](https://github.com/zymk9/yolov5_anime) because they have the same purpose.

On the same dataset with the same parameters (conf=0.001 & iou=0.6), yolov8x6-animeface produces better metrics than the one on yolov5x.

yolov8-animeface:
```
Images  Instances    Box(P        R      mAP50     mAP50-95):
1002       1562      0.957      0.924      0.955      0.534
```

yolov5-anime:

```
Images  Instances    Box(P        R      mAP50     mAP50-95):
 1003       1566      0.778      0.685      0.633      0.232
```

yolov5-anime provides better results when images are resized at 640px, but it still is inferior to yolov8-animeface with the same parameters.
Surprisingly enough, yolov5 is way more confident that yolov8. However, it also has way more false positives.

////// Insert demo here


Based on YOLOv8 by
Jocher, G., Chaurasia, A., & Qiu, J. (2023). Ultralytics YOLO (Version 8.0.0) [Computer software]. https://github.com/ultralytics/ultralytics
