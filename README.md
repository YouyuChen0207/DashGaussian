# DashGaussian: Optimizing 3D Gaussian Splatting in 200 Seconds
### [Webpage](https://dashgaussian.github.io/) | [Paper](https://arxiv.org/pdf/2503.18402) | [arXiv](https://arxiv.org/abs/2503.18402) | [![License: CC BY-NC-SA 4.0](https://img.shields.io/badge/License-CC_BY--NC--SA_4.0-lightgrey.svg)](https://creativecommons.org/licenses/by-nc-sa/4.0/)

The implementation of **DashGaussian: Optimizing 3D Gaussian Splatting in 200 Seconds**, a powerful 3DGS training acceleration method. Accepted by CVPR 2025 (highlight).

In this repository, we show how to plug DashGaussian into [the up-to-date 3DGS implementation](https://github.com/graphdeco-inria/gaussian-splatting). 

## Update History
* 2025.08.16 : A bug in reproduction is fixed. Now DashGaussian works correctly to boost the optimization speed of 3DGS while improving the rendering quality. 

## Environment Setup
To prepare the environment, 

1. Clone this repository. 
	```
	git clone https://github.com/YouyuChen0207/DashGaussian.git
	```
2. Follow [3DGS](https://github.com/graphdeco-inria/gaussian-splatting) to install dependencies. 

	Please notice, that the ```diff-gaussian-rasterization``` module contained in this repository has already been switched to the ```3dgs-accel``` branch for efficient backward computation.

## Run DashGaussian

### Running Comand
Set the data paths in ```scripts/full_eval.sh``` to your local data folder, and run.
```
bash scripts/full_eval.sh
```

### Running Options
In ```full_eval.py```, you can set, 
* ```--dash``` Enable DashGaussian.
* ```--fast``` Use the Sparse Adam optimizer. 
* ```--preset_upperbound``` Set the primitive number upperbound manually for DashGaussian and disable the momentum-based primitive upperbound budgeting method. This option is disabled by default.

### Plug DashGaussian into Other 3DGS Backbones
This repository is an example to plug DashGaussian into 3DGS backbones. 
Search keyword ```DashGaussian``` within the project, you can find all code pieces integrating DashGaussian into the backbone. 

## Results
The following experiment results are produced with a personal NVIDIA RTX 4090 GPU.
The average of rendering quality metrics, number of Gaussian primitives in the optimized 3DGS model, and training time, are reported. 
### [Mipnerf-360 Dataset](https://jonbarron.info/mipnerf360/)
|  Method | Optimizer | PSNR | SSIM | LPIPS | N_GS | Time (min) |
|-----|-----|-----|-----|-----|-----|-----|
| 3DGS | Adam | 27.51 | 0.8159 | 0.2149 | 2.73M | 12.70 |
| 3DGS-Dash | Adam | 27.70 | 0.8201 | 0.2140 | 2.42M | 6.21 | 
| 3DGS-fast | Sparse Adam | 27.33 | 0.8102 | 0.2240 | 2.46M | 7.91 | 
| 3DGS-fast-Dash | Sparse Adam | 27.66 | 0.8167 | 0.2202 | 2.23M | 3.69 |

### [Deep-Blending Dataset](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/datasets/input/tandt_db.zip)
|  Method | Optimizer | PSNR | SSIM | LPIPS | N_GS | Time (min) |
|-----|-----|-----|-----|-----|-----|-----|
| 3DGS | Adam | 29.83 | 0.9069 | 0.2377 | 2.48M | 10.74 |
| 3DGS-Dash | Adam | 29.87 | 0.9061 | 0.2458 | 1.94M | 3.78 | 
| 3DGS-fast | Sparse Adam | 29.48 | 0.9068 | 0.2461 | 2.31M | 6.71 | 
| 3DGS-fast-Dash | Sparse Adam | 30.14 | 0.9085 | 0.2477 | 1.94M | 2.31 |

### [Tanks&Temple Dataset](https://repo-sam.inria.fr/fungraph/3d-gaussian-splatting/datasets/input/tandt_db.zip)
|  Method | Optimizer | PSNR | SSIM | LPIPS | N_GS | Time (min) |
|-----|-----|-----|-----|-----|-----|-----|
| 3DGS | Adam | 23.73 | 0.8526 | 0.1694 | 1.57M | 8.04 |
| 3DGS-Dash | Adam | 24.01 | 0.8514 | 0.1789 | 1.20M | 3.88 | 
| 3DGS-fast | Sparse Adam | 23.78 | 0.8502 | 0.1741 | 1.53M | 6.11 | 
| 3DGS-fast-Dash | Sparse Adam | 24.02 | 0.8519 | 0.1798 | 1.20M | 2.83 |

## Citation
```
@inproceedings{chen2025dashgaussian,
  title={DashGaussian: Optimizing 3D Gaussian Splatting in 200 Seconds},
  author={Chen, Youyu and Jiang, Junjun and Jiang, Kui and Tang, Xiao and Li, Zhihao and Liu, Xianming and Nie, Yinyu},
  booktitle={Proceedings of the Computer Vision and Pattern Recognition Conference},
  pages={11146--11155},
  year={2025}
}
```
