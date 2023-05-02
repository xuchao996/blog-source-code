---
title: install 
date: 2023-03-19
---



> https://zh-v2.d2l.ai/chapter_installation/index.html



## 1. 安装 miniconda



## 2. 使用conda 

### 2.1 初始化conda

```sh
~/miniconda3/bin/conda init
```

### 2.2 创建环境

```sh
conda create --name d2l python=3.9 -y
```

### 2.3 激活d2l环境	

```sh
conda activate d2l
```



## 3.安装pytorch

### 3.1

```sh
pip install torch==1.12.0
pip install torchvision==0.13.0
```

## 3.2

```sh
pip install d2l==0.17.6
```



## 4. 下载代码及运行环境

4.1 

```sh
mkdir d2l-zh && cd d2l-zh
curl https://zh-v2.d2l.ai/d2l-zh-2.0.0.zip -o d2l-zh.zip
unzip d2l-zh.zip && rm d2l-zh.zip
cd pytorch
```



4.2

```sh
jupyter notebook
```



## 5.启停服务

5.1 停止服务

```sh
conda deactivate
```



5.2 启动服务

```sh
$ conda activate d2l
$ jupyter notebook
```

