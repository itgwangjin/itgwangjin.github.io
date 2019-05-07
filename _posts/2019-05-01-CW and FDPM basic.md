---
title: "CW and FDPM basic"
collection: post
permalink: /posts/2019/05/CW and FDPM basic
date: 2019-05-01
tag:
  - CW
  - FDPM
  - optical property
  - calibration
  - SFDI

---

CW와 FDPM의 알고리즘이 어떻게 동작하는지 알아보도록 하자.

# 0. Introduction
우선 왜 CW, FDPM을 쓰는 걸까? 
매질에 빛을 쏴서 해당 매질의 optical property을 얻어내기 위함이다.
> Optical property
> 빛이 매질을 통과할때 흡수되는 정도를 측정한것이 absorption
> 산란되는 정도를 측정하는 것이 scattering이라고 한다.

하지만 빛을 쏴서 photon diode를 통해 얻을 수 있는건 absorption과 scattering이 같이 들어오게 되는데 이것을 분리하는 방법에는 
1. CW(Continue Wave) 
2. TD(Time Domain) 
3. FD(Frequency Domain)

총 3가지 방식으로 분리할 수 있다. 
amplitude와 phase 밖에 없다.
이를 curve fitting, p1 approximation 혹은 steady state 방식으로
optical property를 구할 수 있다.
> Curve fitting
> non-linear상태에서 해당 주어진 output을 가지고 가장 근접한 input을 찾는것.

# 1. CW
CW method는 기본적으로 light source로 부터 $\rho$만큼 떨어진 거리 마다 photon detector를 통해 값을 받아오는 형식이다.

각 떨어진 거리에서 받은 값 phase, amplitude를 통해 optical property를 구한다.
일반적으로 스마트시계에 쓰이는 기법중 하나다.
>Example 
>![
](https://lh3.googleusercontent.com/ikGlCImsnEftSPnWzN48pCrpJhiJ9gfvTr9HiSikVPROsYN2AO7OaVdm8xKwlgB5lci_juJlzJHz "Apple")
<그림 애플워치 뒷면> 2개의 LED, 2개의 photon diode
 
기기마다 고유의 특성($\alpha$)이 있는데 optical property가 부여된 phantom을 통해서 표준화해주는 과정이 반드시 필요하다 이를 Calibration이라고 일컫는다.
Calibration 이후 다른 매질을 측정했을때 정확한값을 가질 수 있는것이다.

## 1) Forward model (=> Calibration)
(1) **준비물** 

Reference phantom (인체와 유사한 $\mu_a$, $\mu_s'$를 지닌 물질)

(2) **Flow**
1. Light source에 600 ~ 1000Mhz modulation을 걸어 phantom에 쏜다.
2. 측정된 Amp를  $A_1$, $A_2$, $A_3$ 라고 하자.
3. phantom의  $\mu_a$, $\mu_s'$와 $f$ 을 [*Rtherory*](https://www.spiedigitallibrary.org/journalArticle/Download?fullDOI=10.1117%2F1.3523616) 공식을 통해  diffuse reflectance값인  R $R_1$, $R_2$, $R_3$을 구한다. 
4. Calibrated Amplitude은 $A_{1}$ $\div$ $R_{1}$ 으로 구한다.
R3까지 Calibrated Amplitude는 총 $R_{c1}$,$R_{c2}$,$R_{c3}$이 나온다.

?? 교수님이 mDOSI를 reference data로 쓰는 부분이 어디지?

## 2) Inverse model (=> apply to real world)
(1) **준비물**

Calibrated Amplitude  $R_{c1}$,$R_{c2}$,$R_{c3}$

(2) **Flow**
1. Light source에 600 ~ 1000Mhz modulation을 걸어 Target에 쏜다.
2. 측정된  Amplitude 1,2,3을  $A_{t1}$, $A_{t2}$, $A_{t3}$ 라고 하자.
3. $A_{t1}$ $\div$ $A_{c1}$으로 $A_{calT1}$ ,  $A_{calT2}$,  $A_{calT3}$를 구한다.
4. $A_{calT1}$, $A_{calT2}$, $A_{calT3}$를 *least square curve fit*에 넣어 $\mu_a$, $\mu_s'$를 구한다.
> wavelength때문에 x6의 $\mu_a$, $\mu_s'$를 구한다.

# 2. FDPM

FDPM의 경우 CW처럼 $\rho$가 많지 않고 한 detector에서만 데이터를 받는다. CW와 동일하게 calibration을 해주는 과정이 필요하다.

## 1) Forward model (=> Calibration)
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

# 3. 번외

SFDI는 공간 주파수에서 frequency 변화를 통해 phase 차이를 얻어낸다
DC값으로 mua값을 구한다.

# 4. 뭐지
하스켈
파렐
푸리에 변환 은 시간에 대한 함수 를 함수를 구성하고 있는 주파수 성분으로 분해하는 작업이다. 음악에서, 악보에 코드를 나타낼 때,
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTkzOTUxNjE3MiwtMzQyNTQ3MDUyLC01OT
QwMjY1LC0xODM4MTM3MjI4LC0xMjIxMzAyMTg1LDExMzM0MTc1
NjMsMTkzNDMwMDY1MiwxNjQ3MDA2NjM2LC0xMTk1MDkzMzgxLD
E5NTcwNDgxMjAsLTk5NjA3MDY2NV19
-->