---


---

<hr>
<p>title: “Deep learning [Nature 521 7553 (436-444)] REVIEW”<br>
collection: post<br>
permalink: /posts/2019/04/Deep learning [Nature 521 7553 (436-444)]_REVIEW<br>
date: 2019-04-03<br>
tag:</p>
<ul>
<li>Deeplearning</li>
<li>overall DNN</li>
<li>CNN</li>
</ul>
<hr>
<p>I think it is good to read the overall flow of Deep learning from Neural net to CNN.   <a href="http://www.cs.toronto.edu/~hinton/absps/NatureDeepReview.pdf">Paper link</a></p>
<h2 id="introduction">0. Introduction</h2>
<p><a href="https://github.com/itgwangjin/Deep-Learning-Papers-Reading-Roadmap#deep-learning-papers-reading-roadmap">Deep Learning Papers Reading Roadmap</a>에서의 첫번째 읽을 논문이다.<br>
Author :  Yann LeCun, Yoshua Bengio &amp; Geoffrey Hinton</p>
<h2 id="abstract">1. Abstract</h2>
<p>Deep learning allows computational models that are composed of multiple processing layers to learn representations of data with multiple levels of abstraction</p>
<ul>
<li>딥러닝은 기본적으로 multiple processing layer로 이루어져 있다.</li>
<li>각 레이어는 다중 레벨의 추상화와 함께 데이터의 특징을 배운다.</li>
</ul>
<p>These methods have dramatically improved the state-of-the-art in speech recognition, visual object recognition, object detection and many other domains such as drug discovery and genomics.</p>
<ul>
<li>이러한 방법으로 최근 음성인식, 물체인식, 물체감지 및 신약 개발 혹은 유전자 분야에서 놀라운 성과를 보이고 있다.</li>
</ul>
<p>Deeplearning discovers intricate structure in large data sets by using the backpropagation algorithm to indicate how a machine should change its internal parameters that are used to compute the representation in each layer from the representation in the previous layer</p>
<ul>
<li>딥러닝은 큰 데이터 조합 에서 backpropagation algorithm을 사용해서 복잡한 구조를 발견한다.</li>
</ul>
<blockquote>
<p>backpropagation이란 어떻게 기계가 내부 파라메터를 바꿔주는지 보여주는것.<br>
내부 파라메터는 이전레이어에서의 특징으로 부터 각 레이어안에서 대표성을 계산하는데 사용된다.</p>
</blockquote>
<p>Deep convolutional nets have brought about breakthroughs in processing images, video, speech and<br>
audio, whereas recurrent nets have shone light on sequential data such as text and speech.</p>
<ul>
<li>CNN(convlutional neural net)은 이미지, 비디오, 음성, 오디오에 큰 기여를 했다.</li>
<li>반면 RNN(recurrent neural net)의 경우 text나 음성같은 연속되는 데이터에서 각광받는다.</li>
</ul>
<h2 id="history-of-deeplearning">2. History of Deeplearning</h2>
<h3 id="conventional-machine-learning">(1) Conventional machine-learning</h3>
<p>원래 machine learning은 raw data에서 natural data로 처리하는 능력에 한계가 있었다.<br>
지난 10년간, 원래 패턴인식 혹은 머신러닝시스템을 구성하는것은 정밀한 engineeering과 feature 추출기를 디자인할만한 해당 분야의 상당한 전문가가 있었어야했다.</p>
<blockquote>
<p><strong>Note.</strong> Feature extrator<br>
raw data(such as the pixel values of an image)에서 적합한 internal represenctaion로 변환시켜주는것 혹은 learning subsystem이 input에 대해서 pattern을 분류하거나 감지해주는것.</p>
</blockquote>
<h3 id="deeplearning의-등장">(2) Deeplearning의 등장</h3>
<ul>
<li>
<p>Representation learning은 raw data를 machine에 input으로 주면 output으로<br>
classfication 혹은 detection에 필요한 대표성을 자동으로 발견해 주는것이다.</p>
</li>
<li>
<p><strong>Deep learning</strong> 이란 Representation learning + multi-levels of representation을 뜻하며<br>
raw data부터 시작해서 각 layer는 simple하지만 비선형성을 가지면서 한 layer에서의 representation을 더 높은 layer로 보낸다.</p>
</li>
<li>
<p>higher layer of representation은 input의 aspects를 증폭시킨다. 왜냐하면 식별(discrimination)하고 무관한 변수(variations)를 숨기기 위해서 필요한 작업이기 때문이다.<br>
ex) An image :</p>

<table>
<thead>
<tr>
<th align="left">단계</th>
<th align="left">Action</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">1.Input</td>
<td align="left">images (Array in pixel values)</td>
</tr>
<tr>
<td align="left">2.First layer</td>
<td align="left">특정한 방향이나 위치에 edges 존재 유무를 특징으로 잡는다(represenct)</td>
</tr>
<tr>
<td align="left">3.Second layer</td>
<td align="left">작은 variations에 관계없이 특정한 배열에 spotting 시킴으로써 장식품(motifs)를 발견한다.</td>
</tr>
<tr>
<td align="left">4.Thrid layer</td>
<td align="left">장식품(motifs)를 유사한 물체의 부분과 일치하는 combination에 조립시킨다.</td>
</tr>
<tr>
<td align="left">5. Subsequent layer</td>
<td align="left">object를 물체의 부분들의 combinations을 통해서 물체를 발견한다.</td>
</tr>
</tbody>
</table><blockquote>
<p>[Point] 이러한 특징을 잡은 layer는 인간이 한것이 아니라.<br>
Data를 통해 일반적인 learning procedure를 통해서 학습한다!</p>
</blockquote>
</li>
</ul>
<h2 id="supervised-learning">Supervised learning</h2>
<p>머신러닝에서 가장 일반적인 form은 supervised learning이다.<br>
우리가 음성, 집, 차, 사람, 동물 분류시스템을 만들수 있다고 상상해보자.</p>
<ol>
<li>큰 집, 차, 사람, 동물의 아주 많은 라벨링된 이미지를 학습시킨다.<br>
-&gt; training동안 machine은 각 category별로 점수화 하여 vector 형태로 준다.</li>
<li>우리는 objective function을 통해서 output score와 원하는 scores의 패턴사이의 error률을 계산합니다.</li>
<li>machine은 조절이 가능한 내부 파라매터(weight)를 에러율을 줄이수 있게 수정합니다.</li>
<li>weight를 조절하기 위해서 learning algorithm은 <em>gradient vector</em>를 계산합니다.</li>
</ol>
<blockquote>
<p>Gradient vector<br>
기울기를 측정함으로써 error가 증가할것인지 감소할것인지 알 수 있다.</p>
</blockquote>
<ol start="5">
<li>weight vector는 gradient vector와 반대 방향으로 조절된다.</li>
</ol>
<h3 id="objective-function">Objective function</h3>
<p>실제로 대부분의 실무자(practitioners)는 stochastic gradient descent(SGD)를 사용한다.</p>
<h4 id="sgdstochastic-gradient-descent">SGD(Stochastic Gradient Descent)</h4>
<ol>
<li>output과 error를 계산</li>
<li>example를 통해 평균 gradient를 계산하고, weight를 적절히 조절한다.</li>
<li>training set으로 부터의 example의 작은세트를 objective function이 줄어드는게 멈출때까지 반복하는것이다.</li>
<li>rkskk</li>
</ol>
<hr>

<table>
<thead>
<tr>
<th align="center">단어</th>
<th align="center">뜻</th>
</tr>
</thead>
<tbody>
<tr>
<td align="center">intricate</td>
<td align="center">복잡한</td>
</tr>
<tr>
<td align="center">surppress</td>
<td align="center">숨기다, 진압하다</td>
</tr>
<tr>
<td align="center">motif</td>
<td align="center">장식품</td>
</tr>
<tr>
<td align="center">applicable to</td>
<td align="center">~에 적당한</td>
</tr>
<tr>
<td align="center">recorrent</td>
<td align="center">되풀이되는</td>
</tr>
<tr>
<td align="center">indicate</td>
<td align="center">나타내다</td>
</tr>
<tr>
<td align="center">discrimination</td>
<td align="center">식별, 차별</td>
</tr>
<tr>
<td align="center">orientation</td>
<td align="center">방향</td>
</tr>
<tr>
<td align="center">knobs</td>
<td align="center">손잡이</td>
</tr>
</tbody>
</table>
