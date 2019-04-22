---
title: "Tensorflow 2.0 환경설정"
collection: post
permalink: /posts/2019/04/tensorflow 2.0 환경설정
date: 2019-04-22
tag:
  - tensorflow 2.0
  - window 10
  - python 3.7
  - CUDA
  - cuDNN

---

연구실에 tensorflow 2.0 를 까는데 일정한 가이드라인이 없는거같아
직접 만들어 보았다.
 
 
# tensorflow 2.0-alpha 설치

## 0. requirment 확인하기
![enter image description here](https://lh3.googleusercontent.com/we1XaiLx80omuwkYKZMSetmo5moOuY3K6iglZqzPna7J-u0mBdejDO2JidBDwkV-Zb6Au5BlY2_H)
## 1. ananconda 설치
![](https://4.bp.blogspot.com/-AxYzinlTdSA/XB9PAAEwkSI/AAAAAAAAA9k/xZQKhvzi9ckUQlfexGfe6NLwnWKbzY3XgCLcBGAs/s1600/anaconda%2B2018-12.png)
### update anaconda & python packages
``` python
>conda update -n base conda
>conda update --all
```

## 2. install CUDA 10.0
-   NVIDIA Cuda Toolkit 설치 : https://developer.nvidia.com/cuda-toolkit-archive
- CUDA_PATH, CUDA_PATH_V10_0 환경변수 설정 

![enter image description here](https://lh3.googleusercontent.com/GutKk8ytJ9mPJg-aoidW3HtFwTIHXpPCf7Vawnkrlynd2t9AxuYjnno9ce0Dzn1r1zfog6YSZhGi)
추가 되어 있다면 넘어간다.

## 3. install cuDNN SDK
- cuDNN 다운로드 : https://developer.nvidia.com/rdp/cudnn-archive
- 압축풀기
- 압축 안의 내용 모두 CUDA_PATH 경로의 폴더에 추가  
> ```shell
> # 기본 path
> C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v10.0
> ```
- 환경변수 추가
``` shell
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\bin  
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\include  
C:\Program Files\NVIDIA GPU Computing Toolkit\CUDA\v9.0\lib
```

## 4. install tensorflow
- 현재 tensorflow 2.0이 python 3.6만 지원하므로 아래와 환경변수 만들기
```shell
conda create -n tf_gpu pip python=3.6 
activate tf_gpu  
```
- pip update, -gpu 깔아주기
```shell
python -m pip install --upgrade pip
pip install tensorflow-gpu==2.0.0-alpha0
```
- jupyter 설치
``` shell
pip install jupyter
```
- 나중에 colab과 연동하려면
``` shell
pip install jupyter_http_over_ws
```

## (optional) Install Python and the TensorFlow package  dependencies

``` shell

```
pip3 install six numpy wheel
pip3 install keras_applications==1.0.6 --no-deps
pip3 install keras_preprocessing==1.0.5 --no-deps
```

## 마무리
``` shell
C:> activate tf_gpu
(tensorflow) C:> python
```
``` python
>>> import tensorflow as tf 
>>> hello = tf.constant('Hello, TensorFlow!') 
>>> sess = tf.Session() 
>>> print(sess.run(hello))
Hello, TensorFlow!
```
위와 같이 잘 나타난다면 성공~! 
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk3NDUxNTg5OSwtMjY3MjUxNTg5XX0=
-->