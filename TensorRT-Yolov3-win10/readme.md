# TRTForYolov3

<a href="https://996.icu"><img src="https://img.shields.io/badge/link-996.icu-red.svg" alt="996.icu" /></a>

## Desc

    tensorRT for Yolov3 （win10）

### Test Enviroments

    win 10
    TensorRT 5.1/5.0.2.6/4.0.1.6
    CUDA 9.0 

### Models

Download the caffe model converted by official model:

+ Baidu Cloud [here](https://pan.baidu.com/s/1VBqEmUPN33XrAol3ScrVQA) pwd: gbue
+ Google Drive [here](https://drive.google.com/open?id=18OxNcRrDrCUmoAMgngJlhEglQ1Hqk_NJ)


If run model trained by yourself, comment the "upsample_param" blocks, and modify the prototxt the last layer as:
```
layer {
    #the bottoms are the yolo input layers
    bottom: "layer82-conv"
    bottom: "layer94-conv"
    bottom: "layer106-conv"
    top: "yolo-det"
    name: "yolo-det"
    type: "Yolo"
}
```

It also needs to change the yolo configs in "YoloConfigs.h" if different kernels.

# build source code


导入vs中，生成解决方案后，将“3rdparty/dll/x64”中"pthreadGC2.dll"和"pthreadVC2.dll"复制到输出文件夹中

# what I do

1.Added multithreading

2.Added tag name

3.Added video inference


# for yolov3-608

## video

./install/runYolov3 --caffemodel=./yolov3_608.caffemodel --prototxt=./yolov3_608.prototxt --display=1 --inputstream=video --videofile=sample_720p.mp4 --classname=coco.names

## cam

./install/runYolov3 --caffemodel=./yolov3_608.caffemodel --prototxt=./yolov3_608.prototxt --display=1 --inputstream=cam --cam=0 --classname=coco.names

## int8

./install/runYolov3 --caffemodel=./yolov3_608.caffemodel --prototxt=./yolov3_608.prototxt --display=1 --inputstream=cam --cam=0 --classname=coco.names --mode=int8 --calib=cal.list

## example


![图片alt](https://raw.githubusercontent.com/talebolano/TensorRT-Yolov3/master/image/example.png)

### Performance

Model | GPU | Mode | Inference Time | FPS
-- | -- | -- | -- | -- |
Yolov3-608 | GTX 1060(laptop)(win10) | float32 | 58ms | 15
Yolov3-608 | GTX 1060(laptop)(win10) | int8 | 33ms | 18




