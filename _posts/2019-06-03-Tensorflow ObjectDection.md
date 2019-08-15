---
title: "CNN in TenorFlow"
collection: post
permalink: /posts/2019/08/CNN in TenorFlow
date: 2019-08-15
tag:
  - tensorflow
  - CNN
---
Kaggle에서 CNN 기본을 배우기 위한 간단한 과제를 풀어보려고 한다.
[https://www.kaggle.com/c/dogs-vs-cats/kernels](https://www.kaggle.com/c/dogs-vs-cats/kernels)


첫번째로 Image를 Trainset과 Validataion set를 나눠보자 
```python
# Tensorflow와 Keras는 이미지를 명ㄷ
from tensorflow.keras.preprocessing.image import ImageDataGenerator

# All images will be rescaled by 1./255.
train_datagen = ImageDataGenerator( rescale = 1.0/255. )
# --------------------
# Flow training images in batches of 20 using train_datagen generator
# --------------------
train_generator = train_datagen.flow_from_directory(train_dir,
                                                    batch_size=20,
                                                    class_mode='binary',
                                                    target_size=(150, 150))     
# --------------------
# Flow validation images in batches of 20 using test_datagen generator
# --------------------
validation_generator =  test_datagen.flow_from_directory(validation_dir,
                                                         batch_size=20,
                                                         class_mode  = 'binary',
                                                         target_size = (150, 150))

```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMzc3MTg5OTksLTExMjM2ODczMF19
-->