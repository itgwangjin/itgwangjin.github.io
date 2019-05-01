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
기기마다 고유의 특성이 있는데 optical property를 알고 있는 phantom을 통해서 표준화해주는 과정이 반드시 필요하다 이를 Calibration이라고 일컫는다.
Calibration 이후 다른 매질을 측정했을때 정확한값을 가질 수 있는것이다.

## 1)Forward model (= Calibration)

system response를 없애주는 과정
### 1. Forward model
\* **system response?** -> 기기의 고유 특성
> Measured Amp    
> Theoretical R   

이 두개를 나눠줌으로써 system response를 구한다.
Target Amp을 system response를 내려서 
Target의 R1, R2, R3 구한다. 

### 2. Inverse model
Input : R1, R2, R3
model : least square curve fit
Output : $\mu_a$, $\mu_s'$ x 6 (wavelength)

# FDPM
- 초기에 알고 있는 값.
	- Reference phantom data : $\mu_a$, $\mu_s'$
	- Measured phantom data : Amp, Phase
	$\mu_a$, $\mu_s'$로 구한 값
- 측정해서 나온 값
	- Measured target data : Amp & phase

FDPM의 경우 CW처럼 $\rho$가 많지 않고 한 detector에서만 데이터를 받는다. CW와 동일하게 calibration을 해주는 과정이 필요하다.

## Forward model (Calibration)
(1) **준비물** 
 Reference phantom (인체와 유사한 $\mu_a$, $\mu_s'$를 지닌 물질)

(2) **Flow**
1. Light source에 50Mhz - 500Mhz modulation을 걸어 phantom에 쏜다.
2. 측정된  Amp와 phase를 $A_{measured}$, $P_{measured}$ 라고 하자.
3. phantom의  $\mu_a$, $\mu_s'$와 $f$ 을 *p1 Approximation* 공식을 통해  theoretical 한 값인 $A_{theoretical}$, $P_{theoretical}$ 구한다. 
4. Calibrated Amplitude은 $A_{measured}$ $\div$ $A_{theoretical}$ 으로 구한다.
5. Calibrated Phase의 경우 $P_{measured}$ $\s$ $P_{theoretical}$ 으로 구한다.

## Inverse model ( apply real world )

(1) **준비물**
Calibrated Amplitude ($A_{calibrated}$) ,  Calibrated Phase ($P_{calibrated}$) 
(2) **Flow**
1. Light source에 50Mhz - 500Mhz modulation을 걸어 Target에 쏜다.
2. 측정된  Amp와 phase를 $A_{target}$ $P_{target}$ 라고 하자.
3. $A_{target}$ $\div$ $A_{calibrated}$
기존에 구한 ca1과 cal2를 각각 나눠주고 빼줌으로써
Amp와 phase를 다시 p1 approximation으로 $\mu_a$, $\mu_s'$를 구한다.

phase를 통해서 mus를 통해 이미 구할수 있으니까 LUT 굳이 필요없다.
단점 시간이 오래걸린다 극복 DNN amp

CW에는 mus를 구할 근거가 마땅히 없다 극복 LUT
잘 안되면 DNN

SFDI 공간 주파수에서 frequency 변화를 통해 위상 차이를 얻어낸다
phase를 iterat
DC값으로 mua값을 구한다.


## FDPM nomalization
CW와 다른점이 얘는 Amp와 phase가 다르다
- Amplitude
기존에 알고
- Phase


p1seminf의 input data는 $\mu_a$, $\mu_s'$, n (frequency)통
n이 frequency 
여기는 빼는것.
DNN은 reverse 모델이니까.
photon 을 매질의 특성을 넣어준것.

<!--stackedit_data:
eyJoaXN0b3J5IjpbMTg2OTMxMzg2NSwtMTExNzc3ODY1MywtMT
I2NDk2NDc1MCwtODEwNzU2ODQ0LC03NDUyMzQyNjksLTkwNzY1
NTI4MSw3NDI2NzQzNDUsMjk1MzAwNzY3LDE3MzUxMzk1ODAsLT
k0ODIxOTg0XX0=
-->