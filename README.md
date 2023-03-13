# PRISE: Demystifying Deep Lucas-Kanade with Strongly Star-Convex Constraints for Multimodel Image Alignment
Demo code for our proposed **PRISE** on GoogleMap, GoogleEarth, and MSCOCO datasets.

## Introduction
We proposed **PRISE** to enforce the neural network to approximately learn a star-convex loss landscape around the ground truth given data to facilitate the convergence of the Deep Lucas-Kanade method to the ground truth through the high dimensional space defined by the network.

<div align=center><img src="https://github.com/swiftzhang125/PRISE/blob/main/image/fig1.png" width="500" height="350" alt="Compared with DeepLK"/></div>



## Requirements
Create a new anaconda environment and install all required packages before runing the code.
```bash
conda create --name prise
conda activate prise
pip install requirements.txt
```


## Dataset
You can follow the dataset preparation [here](https://github.com/placeforyiming/CVPR21-Deep-Lucas-Kanade-Homography). 

Please note that changing the data path if necessary.
```bash
./src/ # modfiy the data_read.py
```


## Usage
To train a model to estimate the homography:
* Step1: Finding a good initialization for the homography estimation
* Step2: Train the PRISE model
```bash
cd src
sh create_checkpoints.py # step1
sh run.sh # step2
```

To see the training loss and test reuslts under:
```bash
cd ./results/<dataset_name>/mu<mu>_rho<rho>_l<lambda_loss>_nsample<sample_noise>/trainig/
```

## Performance
Evaluation results on MSCOCO dataset.
| Method  | PE < 0.1 | PE < 0.5 | PE < 1| PE < 3| PE < 5 | PE < 10 | PE < 20 |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |------------- |------------- |
| SIFT + RANSAC  |  0.00 |  4.70 | 68.32 | 84.21 | 90.32 | 95.26 |  96.55 |
| SIFT + MAGSAC  |  0.00 |  3.66 | 76.27 | 93.26 | 94.22 | 95.32 |  97.26 |
| LF-Net         |  5.60 |  8.62 | 14.20 | 23.00 | 78.88 | 90.18 |  95.45 |
| LocalTrans     | 38.24 | **87.25** | 96.45 | 98.00 | 98.72 | 99.25 | **100.00** |
| DHM            |  0.00 |  0.00 |  0.87 |  3.48 | 15.27 | 98.22 |  99.96 |
| MHN            |  0.00 |  4.58 | 81.99 | 95.67 | 96.02 | 98.45 |  98.70 |
| CLKN           | 35.24 | 83.25 | 83.27 | 94.26 | 95.75 | 97.52 |  98.46 |
| DeepLK         | 17.16 | 72.25 | 92.81 | 96.76 | 97.67 | 98.92 |  99.03 |
| **PRISE**          | **52.77** | 83.27 | **97.29** | **98.44** | **98.76** | **99.31** |  99.33 |

Evaluation results on GoogleEarth dataset.
| Method  | PE < 0.1 | PE < 0.5 | PE < 1| PE < 3| PE < 5 | PE < 10 | PE < 20 |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |------------- |------------- |
| SIFT + RANSAC  |  0.18 |  3.42 |  8.97 | 23.09 | 41.32 | 50.36 | 59.88 |
| SIFT + MAGSAC  |  0.00 |  0.00 |  1.88 |  2.70 |  3.25 | 10.03 | 45.29 |
| DHM            |  0.00 |  0.02 |  1.46 |  2.65 |  5.57 | 25.54 | 90.32 |
| MHN            |  0.00 |  3.42 |  4.56 |  5.02 |  8.99 | 59.90 | 93.77 |
| CLKN           |  **0.27** |  2.88 |  3.45 |  4.24 |  4.32 |  8.77 | 75.00 |
| DeepLK         |  0.00 |  3.50 | 12.01 | 70.20 | 84.45 | 90.57 | 95.52 |
| **PRISE**          |  0.24 | **25.44** | **53.00** | **82.69** | **87.16** | **90.69** | **96.70** |

Evaluation results on GoogleMap dataset.
| Method  | PE < 0.1 | PE < 0.5 | PE < 1| PE < 3| PE < 5 | PE < 10 | PE < 20 |
| ------------- | ------------- | ------------- | ------------- | ------------- | ------------- |------------- |------------- |
| SIFT + RANSAC  |  0.00 |  0.00 |  0.00 |  0.00 |  0.00 |  2.74 |  3.44 |
| SIFT + MAGSAC  |  0.00 |  0.00 |  0.00 |  0.00 |  0.00 |  0.15 |  2.58 |
| DHM            |  0.00 |  0.00 |  0.00 |  1.20 |  3.43 |  6.99 | 78.89 |
| MHN            |  0.00 |  0.34 |  0.45 |  0.50 |  3.50 | 35.69 | 93.77 |
| CLKN           |  0.00 |  0.00 |  0.00 |  1.57 |  1.88 |  8.67 | 22.45 |
| DeepLK         |  0.00 |  2.25 | 16.80 | 61.33 | 73.39 | 83.20 | 93.80 |
| **PRISE**| **17.47** | **48.13** | **56.93** | **76.21** | **80.04** | **86.13** | **94.02** |

## Advanced
To change the hyperparameters:
```bash
cd ./src/ # and modify the settings.py
```
If you are looking for Pytorch implementation of our Star-Convex Constraints
```bash
cd ./py-sc/
```

## Publication
Please cite our papers if you use our idea or code:
```
@inproceedings{zhang2023prise,
  title={PRISE: Demystifying Deep Lucas-Kanade with Strongly Star-Convex Constraints for Multimodel Image Alignment},
  author={Zhang, Yiqing and Huang, Xinming and Zhang, Ziming},
  booktitle={Proceedings of the IEEE/CVF Conference on Computer Vision and Pattern Recognition},
  year={2023}
}
```


