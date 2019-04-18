---
title: "Deep learning [Nature 521 7553 (436-444)] REVIEW"
collection: post
permalink: /posts/2019/04/Deep learning [Nature 521 7553 (436-444)]_REVIEW
date: 2019-04-03
tag:
  - Deeplearning
  - overall DNN
  - CNN
---
I think it is good to read the overall flow of Deep learning from Neural net to CNN.   [Paper link](http://www.cs.toronto.edu/~hinton/absps/NatureDeepReview.pdf)

## 0. Introduction
[Deep Learning Papers Reading Roadmap](https://github.com/itgwangjin/Deep-Learning-Papers-Reading-Roadmap#deep-learning-papers-reading-roadmap)에서의 첫번째 읽을 논문이다.
Author :  Yann LeCun, Yoshua Bengio & Geoffrey Hinton

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

## 2. History of Deeplearning

### (1) Conventional machine-learning
원래 machine learning은 raw data에서 natural data로 처리하는 능력에 한계가 있었다.
지난 10년간, 원래 패턴인식 혹은 머신러닝시스템을 구성하는것은 정밀한 engineeering과 feature 추출기를 디자인할만한 해당 분야의 상당한 전문가가 있었어야했다.
> **Note.** Feature extrator
raw data(such as the pixel values of an image)에서 적합한 internal represenctaion로 변환시켜주는것 혹은 learning subsystem이 input에 대해서 pattern을 분류하거나 감지해주는것.


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
  
  > [Point] 이러한 특징을 잡은 layer는 인간이 한것이 아니라. 
  > Data를 통해 일반적인 learning procedure를 통해서 학습한다!

## 3. Supervised learning
머신러닝에서 가장 일반적인 form은 supervised learning이다.
우리가 음성, 집, 차, 사람, 동물 분류시스템을 만들수 있다고 상상해보자. 
1. 큰 집, 차, 사람, 동물의 아주 많은 라벨링된 이미지를 학습시킨다.
-> training동안 machine은 각 category별로 점수화 하여 vector 형태로 준다.
2. 우리는 objective function을 통해서 output score와 원하는 scores의 패턴사이의 error률을 계산합니다.
3. machine은 조절이 가능한 내부 파라매터(weight)를 에러율을 줄이수 있게 수정합니다. 
4. weight를 조절하기 위해서 learning algorithm은 *gradient vector*를 계산합니다.
> Gradient vector
> 기울기를 측정함으로써 error가 증가할것인지 감소할것인지 알 수 있다.
5. weight vector는 gradient vector와 반대 방향으로 조절된다.

### (1) Objective function
실제로 대부분의 실무자(practitioners)는 stochastic gradient descent(SGD)를 사용한다.
#### - SGD(Stochastic Gradient Descent)
1.  Output과 Error를 계산
2.  Example를 통해 평균 기울기를 계산하고, weight를 적절히 조절한다.
3.  Objective function 의 평균이 더이상 줄어들지 않을때까지 1,2번을 반복한다.

> Stochastic의 의미는 각 small set of examples마다 모든 examples평균 기울기의 측정치

- SGD는 주로 정교한 optimization 기술로  대체로 좋은 가중치 세트를 빠르게  찾아준다.
- 학습이후  시스템의 성능은 test set이라고 불리는 different set으로 측정된다.
- test set은 machine의 일반화 능력을 테스트한다.
- 일반화는 새로운 입력값에 설득력을 더한다. 

## 4. Back propagation
- 현재 머신러닝에서 실무에 나와있는 applications중 다수는 linear classifier를 제일 중점적으로 사용한다.
- 이진 분류기는 feature vector의 구성물의 합을 계산한다.
- 만약 가중화된 합이 **threshold**을 넘으면 input은 특정한 범주에 속하는걸로 분류한다.
- 1960년도 이래로 linear classified는 오직 input을 간단한 범주로 분류할 수 있었고 반공간은 hyperplane에 의해 분별된다.
### (1) Limit of linear classifier
- linear classifier는 위에서 말한 방식과 다르게 중요하게 생각하는 변수와 관련없는 변수를 판단해야하는 input output function을 요구한다.
예를들어
Wolf와 White dog image을 구분하는 모델에서
다른 포즈로 있고 다른 환경에 있는  white dog 사진은 각각 매우 다를지도 모르지만, 같은 위치와 같은 배경에서 white dog와 wolf의 이미지는 매우 유사하게 보일지도 모른다.
- Multi-layer neural network에서 작동하는 shallow한 linear classifier는 input space를 선형으로 분류가능한 데이터로 왜곡할 수 있다.
- 
![
](https://lh3.googleusercontent.com/Pr2c5tDyDU1sozTJh9jbe1862w9ID2SwQ54kiTSkHcXB4blH8dcnXwCoTdfTnuP7I4XWNzWJ32BV "figure1")
- input space에서 규칙적인 격자(left image)에서 hidden unit에 의해 변화를 어떻게 줄 수  있을까?
=> Backpropagation을 이용한다.
b를 보면 알 수 있듯이 $\triangle z$ 
### (2) Backpropagation

##


--- 
 
 
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
knobs	| 손잡이|
elaborate | 정교한 |
carve	| 새기다, 베다|
namely	| 즉
shallow | 얕은|
illustrative example| 설득력있는 예


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE1Mzk3MjUzOTMsODgwMDI2ODAxLC0xMj
EzNTE5MjYxLC0xMDk5ODc0MTgyLC02OTY2MjY0MjIsLTY3NTY4
MjY0OSwxNjc2MDAyMTIsMTY4MDkyNjM3NiwtMTU4NDU5NTA0NS
w2ODg2MzUzMywtOTU3NDQwMTc2LDI3ODY4MzYyOSwtNjQwNTY5
NTUxLC04NDQyMTQ3MjgsLTYxMjIzMDQxOCwxNDQ3NzMyOTQyLC
0xNjg5MDk0MDIyLDkwODM4MjIyMiwtMTMzMzU4MjIyLC0xOTkx
NDUxNTA3XX0=
-->