# Ultralytics Conda 快速入门指南

本指南全面介绍了如何为您的 Ultralytics 项目设置 Conda 环境  

>[原文地址](https://docs.ultralytics.com/zh/guides/conda-quickstart/#note-on-cuda-environment)

## 1.安装Anaconda 或 Miniconda

>[Anaconda](https://www.anaconda.com/)  

## 2.设置 Conda 环境

首先创建一个新的 Conda 环境。打开cmd并运行以下命令：  

``conda create --name ultralytics-env python=3.11 -y``

激活新环境：
``conda activate ultralytics-env``

## 3.安装 Ultralytics

>[Ultralytics](https://anaconda.org/conda-forge/ultralytics)

从 conda-forge 频道安装 Ultralytics 包。执行以下命令：

``conda install -c conda-forge ultralytics``  

如果在启用 CUDA 的环境中工作，最好安装 ultralytics, pytorch和 pytorch-cuda 一起以解决任何冲突

``conda install -c pytorch -c nvidia -c conda-forge pytorch torchvision pytorch-cuda=11.8 ultralytics``

## Tip

### 1.解决安装Ultralytics出现网络问题导致下载中断

使用该命令清除下载缓存，重新下载。

``conda clean --packages --tarballs``

### 2.使用 Libmamba 加速安装

如果您正在寻找加速软件包安装在 Conda 中处理，您可以选择使用 libmamba，一个快速、跨平台且具有依赖感知能力的包管理器，可以作为 Conda 默认求解器的替代方案。

启用 libmamba 作为 Conda 的求解器，您可以执行以下步骤：

1. 安装 conda-libmamba-solver package。  

    如果您的 Conda 版本是 4.11 或更高版本，则可以跳过此步骤，因为 libmamba 默认情况下包含。  

    ``conda install conda-libmamba-solver``

2. 配置 Conda 以使用 libmamba 作为求解器：

    conda config --set solver libmamba

这样,您的 Conda 安装现在将使用 libmamba 作为求解器，这应该会加快软件包的安装过程。
