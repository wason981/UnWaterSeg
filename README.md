# UnWaterSeg--Official Pytorch Implementation
Summary::In the underwater target segmentation project, I was mainly responsible for the model performance comparison experiments, which were analysed by different datasets and metrics (e.g. mIoU, mPrecision, FPS, etc.). During the experiments, I found that the model's frame rate decreases under high-resolution images, and it is difficult to balance accuracy and speed. To solve this problem, I tried to optimise the network structure, use the structure reparameterisation technique, and adjust the depth-separable convolution parameters, which effectively improved the accuracy and real-time performance of the model. The experimental results show that the model's mIoU and FPS on SUIM and TrashCan datasets are significantly improved and outperform the baseline model, which has the value of application to real-time target sensing for underwater robots.

## Requirements
* Linux is recommended for performance and compatibility reasons.
* 64-bit Python 3.8 installation. We recommend Anaconda3 with numpy 1.21 or newer.
* We recommend Pytorch 2.0.1, which we used for all experiments in the project.

* ## 1. Prepare the datasets
You can download the [SUIM] dataset(https://github.com/xahidbuffon/SUIM), [UIIS]([https://github.com/xahidbuffon/SUIM](https://github.com/LiamLian0727/WaterMask)) dataset or [TrashCan](https://conservancy.umn.edu/items/6dd6a960-c44a-4510-a679-efb8c82ebfb7) or use you own dataset for training and inference.
If you need to experiment with your own dataset, you must divide the images and masks into the following directory structure:
| :--- | :----------
|dataset|
| &boxvr;&nbsp;annotations
| &boxv;&nbsp; &boxvr;&nbsp;train
| &boxv;&nbsp; &boxvr;&nbsp;val 
| &boxvr;&nbsp; images
| &boxv;&nbsp; &boxvr;&nbsp;train
| &boxv;&nbsp; &boxvr;&nbsp;val 

### 2. Training
You can modify the config in the main and run
```bash
python main.py
```

### 2. Evaluation
You can run 
```
python summary.py
```
for compute the number of parameters of the computational model and the number of floating-point operations per unit time
And run 
```
python predict.py
```
for single image prediction, camera detection and FPS testing.
run 
```
python get_miou.py
```
for mious evaluation.
