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


# 1.  Image를 Trainset과 Validataion set를 나눠보자
- Tensorflow와 Keras는 유용한게 이미지를 명명된 하위디렉토리에 넣으면 자동으로 label을 지정해준다.

코드를  한번 보자
```python
# 1. ImageDataGenerator를 사용하기 위해서는 인스턴스를 생성해야한다.
from tensorflow.keras.preprocessing.image import ImageDataGenerator
# 2. 다음과 같이 설정된 모습이 있는데, 만약에 nomalization이 되어있지 않다면 rescaling을 해줘야한다.
train_datagen = ImageDataGenerator( rescale = 1.0/255. )
# 3. train
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
eyJoaXN0b3J5IjpbLTE0NjgyODM0ODRdfQ==
-->