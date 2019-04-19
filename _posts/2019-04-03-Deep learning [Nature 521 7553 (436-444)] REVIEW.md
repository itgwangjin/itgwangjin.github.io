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

## 4. linear classifier
- 현재 머신러닝에서 실무에 나와있는 applications중 다수는 linear classifier를 제일 중점적으로 사용한다.
- 이진 분류기는 feature vector의 구성물의 합을 계산한다.
- 만약 가중화된 합이 **threshold**을 넘으면 input은 특정한 범주에 속하는걸로 분류한다.
- 1960년도 이래로 linear classified는 오직 input을 간단한 범주로 분류할 수 있었고 반공간은 hyperplane에 의해 분별된다.
### (1) Limit of linear classifier
- linear classifier는 위에서 말한 방식과 다르게 중요하게 생각하는 변수와 관련없는 변수를 판단해야하는 input output function을 요구한다.
예를들어
- linear classifier 혹은 raw pixels에서 동작하는 어느 shallow한 모델은
같은 자세, 같은 배경의 samoyeds와 wolf를 구분하지 못한다.
(단, 다른 배경, 다른 자세의 samoyeds는 구분을 한다)
- 이것이 왜 shallow한 classifier가 invariance dilemma를 해결하는 특성 추출기를 필요로 하는 이유이다.
> **invariance dilemma**
> 1. translational invariance :이미지 분류 문제에서 알고리즘이 이미지에 있는 개체의 위치가 바뀌더라도 이미지를 분류해 낼 수 있는 능력
> 2. size invariance : 미지 분류 문제에서 알고리즘이 이미지의 크기가 바뀌더라도 이미지를 분류해 낼 수 있는 능력
 > 3. rotational invariance : 이미지 분류 문제에서 알고리즘이 이미지의 방향이 바뀌더라도 이미지를 분류해 낼 수 있는 능력
-  classifiers를 좀더 잘 만들기 위해 generic non-linear features를 사용한다. 일명 kernel methods다.
- 그러나 Gaussian kernel과 함께 떠오른 generic features는  learner가 training examples과 아주멀리 떨어지는것을 허용치 않는다.
### (2) Advantage of deep learning   
- 전통적인 옵션은 직접 좋은 feature 추출기를 디자인하는거고 이제는 좋은 features들이 general-purpose learning 절차만 따라간다면 직접 디자인 하는 것을 피할 수 있다 => 이것이 deep learning의 큰 장점이다.
- deep learning architecture는 간단한 modules의 다발로 이루어진 layer의 다발이다.
- 각 모듈은  input값을 선택성과 대표성의 불변을 증가시킨다.
- 5~20정도 되는 multiple non-linear layers과 함께 시스템은 이제 Samoyeds의작은 디테일도 민감하게 반응하고, 크게 관련없는(변수 ex) 배경, 주변환경)들은    무시한다.


- Multi-layer neural network에서 작동하는 shallow한 linear classifier는 input space를 선형으로 분류가능한 데이터로 왜곡할 수 있다.

![
](https://lh3.googleusercontent.com/Pr2c5tDyDU1sozTJh9jbe1862w9ID2SwQ54kiTSkHcXB4blH8dcnXwCoTdfTnuP7I4XWNzWJ32BV "figure1")
- input space에서 규칙적인 격자(left image)에서 hidden unit에 의해 변화를 어떻게 줄 수  있을까?
=> Backpropagation을 이용한다.
## 5. Backpropagation
- 과거 Researchers들의 목표는 학습이 가능한 multi-layer networks를 통해 사람이 만든 feature들을 대체해야하는 것이였다.
- Deep learning이 나오며 multi-layer 설계자들은 간단 stochastic gradient descent를 통해 학습시킬 수 있었다.
- module들 input과 internal weight의 함수가 상대적으로 부드러워지고 이를 
미분이 가능해지자 chain rule for derivatives를 이용하여 backpropagation를 실현 시켰다. 
- module의 output에 관한 기울기로 부터  input에 관한 목적함수로 즉, 반대로 계산이 가능하다는 점이다.
![
](https://lh3.googleusercontent.com/FhHSkXVOl4nC4KNMVBz9vh5vmamamUNfHCYz6AE6X9JFA5IFwSMGI3ofQ6NJWH5MkD4xoyWGXsvf "backpropagation")
- backpropagation 방정식은 모든 모듈들을 통해서 output에서 input으로 모든 모듈을 통해 기울기를  전파한다. 
- 일단 이러한 기울기가 계산되면, 이것은 각 weight에 대해서 gradient를 계산할 수 있다.
- 한 layer에서 다음 layer로 넘어갈때 각 유닛들은 이전 layer의 가중치(weight)들의 합을 non-linear function을 통해서 결과를 계산한다.
- 현재 대부분 non-linear function에는 ReLU(Rectified Linear Unit)라고 불리는 
> **ReLU**
> $f(z) = max(z,0)$라는 형태의 non-linear activation function

- 지난 수십년동안 neural nets는 $tanh(z)$ or Sigmoid ${1 \over 1+e^-z}$와 같은 형태를 띄는 activation function을 썼었다.
- 그러나 ReLU가 일반적으로 많은 layer에서 빠르고 결과적으로 unsupervised pre-training을 제외하곤 supervised network에서 좋은 성능을 나타냈다.
- input layer, output layer의 유닛은 일반적으로 hidden units라고 부른다.
-  The hidden layers는 non-linear에 있는 input를 왜곡시킬수도 있다고 보았기 때문에 카테고리는 마지막 레이어에 의해서 선형적으로 분할이 가능하다.
- 1990년도에 neural nets은 poor local minima 문제에 빠졌기 때문에 학계에서 무시당했었다.
- 실제로 poor local minima는 큰 networks에서는 드문 문제이다
- 최근 theoretical하고 empirical한 결과들은 local minima는 일반적으로 심각한 문제가 아님을 나타낸다.
- gradient가 0인 많은 saddle point로 구성되어 있다지만
분석은 오직 아래로 내려가는 방향의 saddle point가 현재 큰 수에서 나타나고 있지만 그들 중 대부분은 objective funcion의 값과 매우 유사하다.
그러므로 saddle points중 algorithm이 멈추는 문제는 별로 중요하지 않다.

## 뭐하지
- deep feedforward networks의 관심은 2006년도에 다시 살아났따. researcher들이 CIFAR(Canadian Institute for Advanced Research)에 의해 모여졌기 때문이다.
- researcher들은 unsupervised learning 절차를 소개했다. 이 절차는 특성 검출기에서 labeling 된 데이터를 요구하지 않는 layers를 만들 수 있다.
- 각 layers에서 특성을 배우는 layer들에서의 목적은 재구성할수 있거나 특성 검출기의 활동을 모델링하는 것이다.
- pre-training된 layer는 재구성 objective를 사용하는 더 복잡해진 특성검출기에 의해 deep network의 weights는 초기에 sensible한 values를 설정할 수 있었다.
- output의 마지막 layer는 network의 처음부터 더해지고 전체 deep system은 기본 backpropagation을 사용하여 weight를 튜닝한다.
- 이 방식은 손글씨 인식이나 보행자 인식에서 눈에 띄게 잘 작동한다.(labelled data가 매우 제한적일때)

- 첫번제 pre training approach의 주요 application은 speech recognition이고 이것은 GPU등장으로 인해서 기존보다 10~ 20배 빠르게 사용할 수 있다.
- 2009년에 위와 같은 접근법은 음파로부터 추출된 계수의 짧은 시간 windows를 음성의 다양한 단편을 위한 확률 set에 mapp ing시키는데 사용되었다.
이것은 기존에 녹음없이 음성인식하는 방식은 적은 단어만 음성을 녹음시키고 인식하는 방식이 였는데 Deep learning의 탄생으로 많은 단어를 처리 수 있었다.
- 2012년에는 주요 speech groups이 많이 개발되었고 이미 android에 배치 되었었다.
- 작은 데이터셋을 위해 unsupervised pre-training은 overfitting을 방지했고 결과적으로 labelling된 sxamples 의 수가 적을떄 아주 좋은 성능을 냈다.
- 이리하여 deep learning이 재건되었고 이것은 pr-training stage는 small data set만큼은 잘 작동한다는 것을 알 수 있었다.
- 그러나 한 deep하고 feedforward한 network type에서 인접한 layers들 사이로 fully connected한 

## CNN의 등장
[참고할것1](https://hamait.tistory.com/535)
[참고할것2](

CNN의 등장은 많은 Computer vision에서의 현실적인 문제를 해결했다.
### (1) CNN의 특징
Convolution Neural Network는 multiple arrays 형태로 구성되어 있다. 

- 예를 들어.
colour image는 3개의 2D array로 구성되어 있다. 
여기에는 pixel 마다 RGB와 같은 3개의 채널내의 세기 정도가 포함되어 있다.

많은 data 양상(modality)은 multiple array의 형태에 있다.
- 1D :  language와 같은 sequences를 나타낸다.
- 2D : images 혹은 audio spectrograms를 나타낸다.
- 3D : video 혹은 volumetric images를 나타낸다.

CNN에는 총 4가지의 주요 ideas가 들어간다.
1. local connections
2. shared weight
3. pooling
4. the use of many layers

일반적인 CNN의 구조는 stage의 연속이다.
첫째로 몇몇 stages는 2가지의 type으로 구성되어있는데 
convolutional layers와 pooling layer이다.

convolutional layer내 units들은 feature maps안에 생성된다. 각각 unit들은 filter bank라고 불리는 weights의 세트를 통해 이전 레이어의 특징 맵안의 local patches와 연결되어 있다.

weight이 적용된 local 하브이 결과는 ReLU와 같은 non-linearity를 통과한다.
feature map내 모든 units은 같은 filter bank를 공유한다.
단, 한 layer내 다른 feature maps은 다른 filter bank를 사용한다.

CNN은 구조가 2배 인 이유는
첫째로 값들의  local groups은 종종 높게 연관된어있고
독특한 local motifs를 형성한다.
둘째로 images와 다른 신호의 local statistics의 위치는 변하지 않는다. 다시 말하면 만약 motif가 이미지의 한 부분에 있다면 이것은 어디서든 나타날 수 있다.
그러므로 다른 위치에 있는 units은 같은 weight를 공유하고 다른 array의 부분에서 같은 패턴을 발견한다.

수학적으로 feature map에 의해 수행된 연산자를 필터링은 별개의 convolution이다. 그러므로 이름이다.

비록 convolution layer의 역할이 이전 layer로 부터의 features의 접합을 발견하는것일지라도,
**pooling layer**는 의미상으로 비삿한 features를 한개로 합쳐주는 역할을 한다. 왜냐하면 motif를 형성한 features 의 상대적인 위치는 약간 달라질수도 있고

확실하게 motif를 발견하는것은 각 feature의 위치를 coarse-graining(굵게 나뭇결처럼 내는것)하는 것으로 끝낼 수있다.
### (2) pooling
일반적으로 pooling unit은 한 feature map내 units의 local 부분의 최대값을 계산한다.

인접한 pooling units는 input을 patch로 부터 가져옵니다. patch는 1 row 혹은 col 보다 더 이동되었고 그래서 representation의 차원을 줄이고   왜곡의 불변성을 만듭니다.  

convolution, non-linearity, pooling stages 이후  더 convolutional하고 fully-connected layers가 나타난다.

CNN을 통한 Backpropagation 기울기는 일반 deep network로 한것 만큼 간단하다 모든 filter banks내 모든 가중치는 trained될 수 있다.

deep neural networks는 많은 natural 시그널이 계층구조로 되어있다는 특성을 활용한다.
> 계층구조 의미는 higher-level 특성이 lower-level의 특성으로 구성된걸로 이루어 졌다는것을 뜻한다.

- 예를들어 motifs 이미지에서
1. 모서리의 loocal combinations로 motifs를 형성 
2. 형성된 motifs로 parts를 조립
3. 조립된 parts로 object를 형성한다.

pooling은 이전 레이어에서의 요소가 위치와 외형이 다를 경우에만 아주 조금 다른것의 대표성을 허용한다.

CNN에서의 convolutional layer와 pooling layer는 직접적으로 classic 
[ 이후 CNN에 대한 역사는 생략하고 바로 image understanding with deep convolutional network로 넘어가겠습니다.]

### Image understanding with deep convolutional networks



- 


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
illustrative example| 설득력있는 예 |
with respect to | ~에 대한|

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTk5Njc4NDUxMiw1MTcwOTI0ODcsMTc1OD
gzNTk1MSwxNzk3NjU0MjcyLC0xMjQ4NzkwMzU4LDU5MTA2NDQ1
NiwyMDMxMjk0MjAxLC0xOTIwNjA3MDk5LC03MzA3Mjg5MzcsMT
c4Mjg0Nzc1MywxNjU1NDg3MzU2LDU0MzE4MTc1NiwxOTg0OTI3
NzIyLC0yMTUxNzI1MSwxNzM4MjkwNDUsNzMwNTgwNjYsLTc1MD
k0OTM0MCwxMjY5NTYwNDg3LDE1MDU1NTM5MiwtNDg2NjcxMTJd
fQ==
-->