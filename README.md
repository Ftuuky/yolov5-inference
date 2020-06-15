## Introduction

This repository is a fork from [**Ultralytics' repository**](https://github.com/ultralytics/yolov5) for YOLOv5 open-source object detection method. Please check original repo for information on pretrained checkpoints and tutorials on how to reproduce their environment or train with custom data. Main changes are a focus on inference only and ensuring it works in Windows 10.

YOLOv5 provides sota realtime object dectection up to 140 FPS. For more information see the [Roboflow's blog post](https://blog.roboflow.ai/yolov5-is-here/) and guide to [train it on a custom dataset](https://blog.roboflow.ai/how-to-train-yolov5-on-a-custom-dataset/). This [HackerNews]() thread provides additional insights and potential naming controversy. 

This repo was tested in Windows 10 Home (Version 2004) with Nvidia GeForce RTX 2060.

**Credit to Joseph Redmon for YOLO:** https://pjreddie.com/darknet/yolo/.


## Pretrained Checkpoints

The release of YOLOv5 includes five different models sizes: YOLOv5s (smallest), YOLOv5m, YOLOv5l, YOLOv5x (largest).

Ensure you have downloaded the pretrained checkpoints ([GDrive link](https://drive.google.com/drive/folders/1zzc230IK3s0AB3Pvi2UF30JQYDm2rDpW?usp=sharing)) or from the [original repo links](https://drive.google.com/drive/folders/1Drs_Aiu7xx6S-ix95f9kNsA6ueKRpN2J).

This code does not automatically download any models, please download the pretrained checkpoints from link. There's a [tradeoff](https://user-images.githubusercontent.com/26833433/84200349-729f2680-aa5b-11ea-8f9a-604c9e01a658.png) between AP and latency: larger models are more precise but exhibit slower inference. 


## Requirements

Setting up a virtual environment is recommended.

With Python 3.7 or later and CUDA 10.1 on Windows 10, install `torch==1.5` and `torchvision==0.6`. To install run:

```bash
$ pip install torch==1.5.0+cu101 torchvision==0.6.0+cu101 -f https://download.pytorch.org/whl/torch_stable.html
```

Once that, install all `requirements.txt` dependencies. Run the following:

```bash
$ pip install -U -r requirements.txt
```


## Inference

Inference can be run on images or videos but also directly from webcam, rtsp or http streaming links. Results are saved to `./inference/output`.

```bash
$ python detect.py --source file.jpg  # image 
                            file.mp4  # video
                            ./dir  # directory
                            0  # webcam
                            rtsp://170.93.143.139/rtplive/470011e600ef003a004ee33696235daa  # rtsp stream
                            http://qthttp.apple.com.edgesuite.net/1010qwoeiuryfg/sl.m3u8  # http stream
```

To run inference on examples in the `./inference/images` folder:

```bash
$ python detect.py --source ./inference/images/ --weights yolov5x.pt --conf 0.4
Namespace(agnostic_nms=False, augment=False, classes=None, conf_thres=0.4, device='', fourcc='mp4v', half=False, img_size=640, iou_thres=0.5, output='inference/output', save_txt=False, source='./inference/images/', view_img=False, weights='yolov5x.pt')
Using CUDA device0 _CudaDeviceProperties(name='GeForce RTX 2060', total_memory=6144MB)

image 1/5 inference\images\bus.jpg: 640x512 4 persons, 1 buss, Done. (0.072s)
image 2/5 inference\images\dog.jpg: 448x640 1 persons, 1 dogs, 1 couchs, Done. (0.057s)
image 3/5 inference\images\fashion.jpg: 640x448 2 persons, 2 handbags, Done. (0.058s)
image 4/5 inference\images\tokyo.jpg: 512x640 6 persons, 3 handbags, 3 ties, 1 books, Done. (0.056s)
image 5/5 inference\images\zidane.jpg: 384x640 2 persons, 2 ties, Done. (0.047s)
Results saved to \inference\output
```

<img src="https://user-images.githubusercontent.com/26833433/83082816-59e54880-a039-11ea-8abe-ab90cc1ec4b0.jpeg" width="500">  
