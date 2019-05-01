---
title: " CW and FDPM basic"
collection: post
permalink: /posts/2019/05/ CW and FDPM basic
date: 2019-05-01
tag:
  - absorption
  - scattering
  - FDPM
  - Frequency domain
  - 
---
CW와 FDPM의 알고리즘이 어떻게 동작하는지 알아보도록 하자.
우선 왜 CW, FDPM을 쓰는 걸까? 매질에 빛을 쏴서 해당 매질의 optical property ( $\mu_a$,  $\mu_s'$)을 얻어내기 위함이다.
매질의 특성이라 함은 $mu_a$,  $mu_s'$을 의미한다.
하지만 빛을 쏴 얻을 수 있는건 amp와 phase 밖에 없다.
이를 curve fitting 혹은 p1approximation, steady state 방식으로
optical property를 구할 수 있는데 구하기 전 반드시 해줘야 할 부분이 
Calibration이다.
> Curve fitting
> non-linear상태에서 해당 주어진 output을 가지고 가장 근접한 input을 찾는것.
> 
# 1. CW
CW method는 기본적으로 light source로 부터 $\rho$만큼 떨어진 거리 마다 photon detector를 통해 값을 받아오는 형식이다.
기기마다 고유의 특성이 있는데 optical property가 부여된 phantom을 통해서 표준화해주는 과정이 반드시 필요하다 이를 Calibration이라고 일컫는다.
Calibration 이후 다른 매질을 측정했을때 정확한값을 가질 수 있는것이다.

## 1) Forward model (= Calibration)
(1) **준비물** 

Reference phantom (인체와 유사한 $\mu_a$, $\mu_s'$를 지닌 물질)

(2) **Flow**
1. Light source에 600 ~ 1000Mhz modulation을 걸어 phantom에 쏜다.
2. 측정된 Amp를  $A_1$, $A_2$, $A_3$ 라고 하자.
3. phantom의  $\mu_a$, $\mu_s'$와 $f$ 을 [*Rtherory*](https://www.spiedigitallibrary.org/journalArticle/Download?fullDOI=10.1117%2F1.3523616) 공식을 통해  diffuse reflectance값인  R $R_1$, $R_2$, $R_3$을 구한다. 
4. Calibrated Amplitude은 $A_{1}$ $\div$ $R_{1}$ 으로 구한다.
R3까지 Calibrated Amplitude는 총 $R_{c1}$,$R_{c2}$,$R_{c3}$이 나온다.

## 2) Inverse model (=> apply to real world)
Calibrated Amplitude  $R_{c1}$,$R_{c2}$,$R_{c3}$

# 2. FDPM

FDPM의 경우 CW처럼 $\rho$가 많지 않고 한 detector에서만 데이터를 받는다. CW와 동일하게 calibration을 해주는 과정이 필요하다.

## 1) Forward model (Calibration)
(1) **준비물** 
 Reference phantom (인체와 유사한 $\mu_a$, $\mu_s'$를 지닌 물질)

(2) **Flow**
1. Light source에 50Mhz - 500Mhz modulation을 걸어 phantom에 쏜다.
2. 측정된  Amp와 phase를 $A_{measured}$, $P_{measured}$ 라고 하자.
3. phantom의  $\mu_a$, $\mu_s'$와 $f$ 을 *p1 Approximation* 공식을 통해  theoretical 한 값인 $A_{theoretical}$, $P_{theoretical}$ 구한다. 
4. Calibrated Amplitude은 $A_{measured}$ $\div$ $A_{theoretical}$ 으로 구한다.
5. Calibrated Phase의 경우 $P_{measured}$ $-$ $P_{theoretical}$ 으로 구한다.

## 2) Inverse model (=> apply to real world )

(1) **준비물**

Calibrated Amplitude ($A_{c}$) ,  Calibrated Phase ($P_{c}$) 

(2) **Flow**
1. Light source에 50Mhz - 500Mhz modulation을 걸어 Target에 쏜다.
2. 측정된  Amp와 phase를 $A_{target}$ $P_{target}$ 라고 하자.
3. $A_{target}$ $\div$ $A_{c}$으로 $A_{calT}$ , 
$P_{target}$ $-$ $P_{c}$으로 $P_{calT}$ 를 구한다.
4. $A_{calT}$, $P_{calT}$를 다시 *p1 Approximation*에 넣어 $\mu_a$, $\mu_s'$를 구한다.
> phase를 통해서 $\mu_s$는 이미 구할수 있다
> Deep learning은 4번의 *p1 Approximation*를 대체한다.

## 3) Feature

장점 : CW에는 $\mu_s$를 구할 근거가 마땅히 없어 LUT로 구해야한다.
단점 : Inverse model의 시간이 오래걸린다

SFDI 공간 주파수에서 frequency 변화를 통해 위상 차이를 얻어낸다
phase를 iterat
DC값으로 mua값을 구한다.


<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc5MjQ5NTY4MywtODY2NTA1MjM5LC0xMT
E3Nzc4NjUzLC0xMjY0OTY0NzUwLC04MTA3NTY4NDQsLTc0NTIz
NDI2OSwtOTA3NjU1MjgxLDc0MjY3NDM0NSwyOTUzMDA3NjcsMT
czNTEzOTU4MCwtOTQ4MjE5ODRdfQ==
-->