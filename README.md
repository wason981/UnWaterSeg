# UnWaterSeg--Official Pytorch Implementation
**Abstract**:In the underwater target segmentation project, I was mainly responsible for the model performance comparison experiments, which were analysed by different datasets and metrics (e.g. mIoU, mPrecision, FPS, etc.). During the experiments, I found that the model's frame rate decreases under high-resolution images, and it is difficult to balance accuracy and speed. To solve this problem, I tried to optimise the network structure, use the structure reparameterisation technique, and adjust the depth-separable convolution parameters, which effectively improved the accuracy and real-time performance of the model. The experimental results show that the model's mIoU and FPS on SUIM and TrashCan datasets are significantly improved and outperform the baseline model, which has the value of application to real-time target sensing for underwater robots.

## Requirements
* Linux is recommended for performance and compatibility reasons.
* 64-bit Python 3.8 installation. We recommend Anaconda3 with numpy 1.21 or newer.
* We recommend Pytorch 2.0.1, which we used for all experiments in the project.

## 1. Prepare the datasets
You can download the [SUIM](https://github.com/xahidbuffon/SUIM) dataset, [UIIS](https://github.com/LiamLian0727/WaterMask)dataset or [TrashCan](https://conservancy.umn.edu/items/6dd6a960-c44a-4510-a679-efb8c82ebfb7) or use you own dataset for training and inference.
If you need to experiment with your own dataset, you must divide the images and masks into the following directory structure:
| file path                                                                              | &nbsp;
|:---------------------------------------------------------------------------------------| :----------
| dataset                                                                                | Annotations path
| &boxv;&nbsp; &boxvr;&nbsp;train                                                        | Annotations training set
| &boxv;&nbsp; &boxur;&nbsp;val                                                          | Annotations testing set
| &boxvr;&nbsp;images                                                                    | Original Image 
| &ensp;&ensp; &boxvr;&nbsp;train                                                        | Original Image training set
| &ensp;&ensp; &boxvr;&nbsp;val                                                          | Original Image testing set
| 

### 2. Training
The dataset that has been prepared for this purpose may be used directly:
```bash
python main.py
```
Or you can comment the configuration line in `train.py` to accommodate your dataset.

### 2. Evaluation
You can run 
```
python summary.py
```
To predict single images, multiple images, videos or calculate fps,  modify the configaration in `predict.py`:
```bash
pred_cfg = dict(
    # ---------- 预测模式的参数 ----------
    # predict, dir_predict, fps, video
    mode="fps",  # predict, dir_predict, fps, video
    mix_type=1,  # 0混合, 1仅原图, 2仅原图中的目标_扣去背景
    # ---------- 深度卷积神经网络模型的超参数 ----------
    model_path=path to model,
    input_shape=input shape,
    num_classes=class number,
    name_classes=class name,
    # ---------- 单张图片预测 ----------
    img_path=path to image,
    img_save_path=path to save,
    # ---------- 多张图片预测 ----------
    dir_origin_path=path to images,
    dir_save_path=path to save,
    # ---------- fps计算模式 ----------
    test_interval=1000,  # image test interval
    fps_image=path to image,  # image root
    # ---------- 视频或摄像头预测 ----------
    video_path=path to videos,
    video_save_path=path to save,
)
```
and run:
```
python predict.py
```
To verify the miou of a model, modify the configaration in `get_miou.py`:
```bash
val_cfg = dict(
    description="model validation",
    # ---------- 验证模式的参数 ----------
    miou_mode=0,  # 0, 1, 2
    mix_type=1,  # 0混合, 1仅原图, 2仅原图中的目标_扣去背景 get_miou不起作用
    # ---------- 卷积模型的参数 ----------
    model_path=path to your model,
    aux_branch=False,
    num_classes=class number,
    name_classes=class name,
    input_shape=input shape,
    # ---------- 文件夹的位置参数 ----------
    dataset_path=path to your dataset,
    save_file_dir==path to save result,
)
```
and run:
```
python get_miou.py
```
for mious evaluation.
