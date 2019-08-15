---
title: "CNN in TenorFlow"
collection: post
permalink: /posts/2019/08/CNN in TenorFlow
date: 2019-08-15
tag:
  - tensorflow
  - CNN
---

```python
from tensorflow.keras.preprocessing.image import ImageDataGenerator

# All images will be rescaled by 1./255.
train_datagen = ImageDataGenerator( rescale = 1.0/255. )
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTIwMjM5MzM2NDksLTExMjM2ODczMF19
-->