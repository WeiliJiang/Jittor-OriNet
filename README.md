## Notes
We've re-implemented our proposed **Ori-Net**, a direction-guided neural network model, using the [Jittor](https://cg.cs.tsinghua.edu.cn/jittor/) framework. **Ori-Net** aims to improve the connectivity of coronary artery segmentation in CCTA images. **Jittor** is a deep learning framework built entirely on just-in-time (JIT) compilation, internally utilizing innovative meta-operators and a unified computation graph. Its meta-operators are as easy to use as NumPy but can perform more complex and efficient operations. For better compatibility, we still use [Torchio](https://torchio.readthedocs.io/index.html) for efficient loading, preprocessing, augmentation, and patch-based sampling of 3D medical images. You can find the full PyTorch-based version of our model at https://github.com/WeiliJiang/Ori_Net.

## Requirements
* jittor 1.3.9.2
* torchio<=0.18.20
* python>=3.6

## Notice
* You can modify **hparam.py** to determine whether 2D or 3D segmentation and whether multicategorization is possible.
* We provide algorithms for almost all 2D and 3D segmentation.
* This repository is compatible with almost all medical data formats(e.g. nii.gz, nii, mhd, nrrd, ...), by modifying **fold_arch** in **hparam.py** of the config. **I would like you to convert both the source and label images to the same type before using them, where labels are marked with 1, not 255.**
* If you want to use a **multi-category** program, please modify the corresponding codes by yourself. I cannot identify your specific categories.
* Whether in 2D or 3D, this project is processed using **patch**. Therefore, images do not have to be strictly the same size. In 2D, however, you should set the patch large enough.

## Prepare Your Dataset
### Example1
if your source dataset is :
```
source_dataset
├── source_1.mhd
├── source_1.zraw
├── source_2.mhd
├── source_2.zraw
├── source_3.mhd
├── source_3.zraw
├── source_4.mhd
├── source_4.zraw
└── ...
```

and your label dataset is :
```
label_dataset
├── label_1.mhd
├── label_1.zraw
├── label_2.mhd
├── label_2.zraw
├── label_3.mhd
├── label_3.zraw
├── label_4.mhd
├── label_4.zraw
└── ...
```

then your should modify **fold_arch** as **\*.mhd**, **source_train_dir** as **source_dataset** and **label_train_dir** as **label_dataset** in **hparam.py**

### Example2
if your source dataset is :
```
source_dataset
├── 1
    ├── source_1.mhd
    ├── source_1.zraw
├── 2
    ├── source_2.mhd
    ├── source_2.zraw
├── 3
    ├── source_3.mhd
    ├── source_3.zraw
├── 4
    ├── source_4.mhd
    ├── source_4.zraw
└── ...
```

and your label dataset is :
```
label_dataset
├── 1
    ├── label_1.mhd
    ├── label_1.zraw
├── 2
    ├── label_2.mhd
    ├── label_2.zraw
├── 3
    ├── label_3.mhd
    ├── label_3.zraw
├── 4
    ├── label_4.mhd
    ├── label_4.zraw
└── ...
```

then your should modify **fold_arch** as **\*/\*.mhd**, **source_train_dir** as **source_dataset** and **label_train_dir** as **label_dataset** in **hparam.py**

## CCTA data_processing

python CCTA_data_process.py

## Training
* without pretrained-model
```
set hparam.train_or_test to 'train'
python main.py
```
* with pretrained-model
```
set hparam.train_or_test to 'train'
python main.py -k True
```
  
## Inference
* testing
```
set hparam.train_or_test to 'test'
python main.py
```

## Tutorials
* https://www.bilibili.com/video/BV1gp4y1H7kq/

### Metric
- [x] metrics.py to evaluate your results
