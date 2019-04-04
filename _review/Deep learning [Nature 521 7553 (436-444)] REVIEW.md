---
title: "Deep learning [Nature 521 7553 (436-444)] REVIEW"
collection: review
type: Deep learning paper
permalink: /review/Deep learning [Nature 521 7553 (436-444)]_REVIEW
date: 2019-04-03
tag:
  - Deeplearning
  - overall DNN
  - CNN
---

# Deep learning

[Paper link](http://www.cs.toronto.edu/~hinton/absps/NatureDeepReview.pdf)
Author :  Yann LeCun, Yoshua Bengio & Geoffrey Hinton

## 0. Introduction
[Deep Learning Papers Reading Roadmap](https://github.com/itgwangjin/Deep-Learning-Papers-Reading-Roadmap#deep-learning-papers-reading-roadmap)에서의 첫번째 읽을 논문이다.
DNN부터 CNN까지 전반적인 Deep learning의 흐름을 읽고 가기에 좋다고 생각한다.

---

## 1. Abstract
Deep learning allows computational models that are composed of multiple processing layers to learn representations of data with multiple levels of abstraction
- 딥러닝은 기본적으로 multiple processing layer로 이루어져 있다.
- 각 레이어는 다중 레벨의 추상화와 함께 데이터의 특징을 배운다.

These methods have dramatically improved the state-of-the-art in speech recognition, visual object recognition, object detection and many other domains such as drug discovery and genomics.
- 이러한 방법으로 최근 음성인식, 물체인식, 물체감지 및 신약 개발 혹은 유전자 분야에서 놀라운 성과를 보이고 있다.

Deeplearning discovers intricate structure in large data sets by using the backpropagation algorithm to indicate how a machine should change its internal parameters that are used to compute the representation in each layer from the representation in the previous layer
- 딥러닝은 큰 데이터 조합 에서 backpropagation algorithm을 사용해서 복잡한 구조를 발견한다.
> backpropagation이란 어떻게 기계가 내부 파라메터를 바꿔주는지 보여주는것.
내부 파라메터는 이전레이어에서의 특징으로 부터 각 레이어안에서 대표성을 계산하는데 사용된다.

Deep convolutional nets have brought about breakthroughs in processing images, video, speech and
audio, whereas recurrent nets have shone light on sequential data such as text and speech.
- CNN(convlutional neural net)은 이미지, 비디오, 음성, 오디오에 큰 기여를 했다.
- 반면 RNN(recurrent neural net)의 경우 text나 음성같은 연속되는 데이터에서 각광받는다.

---
## 2. History of Deeplearning

### (1) Conventional machine-learning
원래 machine learning은 raw data에서 natural data로 처리하는 능력에 한계가 있었다.
지난 10년간, 원래 패턴인식 혹은 머신러닝시스템을 구성하는것은 정밀한 engineeering과 feature 추출기를 디자인할만한 해당 분야의 상당한 전문가가 있었어야했다.
> **Note.** Feature extrator
raw data(such as the pixel values of an image)에서 적합한 internal represenctaion로 변환시켜주는것 혹은 learning subsystem이 input에 대해서 pattern을 분류하거나 감지해주는것.

---
### (2) Deeplearning의 등장

- Representation learning은 raw data를 machine에 input으로 주면 output으로
classfication 혹은 detection에 필요한 대표성을 자동으로 발견해 주는것이다.
- **Deep learning** 이란 Representation learning + multi-levels of representation을 뜻하며
raw data부터 시작해서 각 layer는 simple하지만 비선형성을 가지면서 한 layer에서의 representation을 더 높은 layer로 보낸다.
- higher layer of representation은 input의 aspects를 증폭시킨다. 왜냐하면 식별(discrimination)하고 무관한 변수(variations)를 숨기기 위해서 필요한 작업이기 때문이다.
ex) An image :
  
  |단계 | Action|
  |:--|:---|
  |1.Input|images (Array in pixel values)|
  |2.First layer| 특정한 방향이나 위치에 edges 존재 유무를 특징으로 잡는다(represenct)|
  |3.Second layer|작은 variations에 관계없이 특정한 배열에 spotting 시킴으로써 장식품(motifs)를 발견한다. |
  |4.Thrid layer| 장식품(motifs)를 유사한 물체의 부분과 일치하는 combination에 조립시킨다.|
  |5. Subsequent layer| object를 물체의 부분들의 combinations을 통해서 물체를 발견한다.|
  




----
  
|단어|뜻|
:----:|:---:|
intricate| 복잡한|
surppress| 숨기다, 진압하다|
motif| 장식품|
applicable to | ~에 적당한|
recorrent| 되풀이되는|
indicate| 나타내다|
discrimination | 식별, 차별|
orientation | 방향|
  
