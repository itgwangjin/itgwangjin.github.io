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
우선 왜 CW, FDPM을 쓰는 걸까? 매질에 빛을 쏴서 해당 매질의 optical property ( $\mu_a$,  $\mu_s'$ )을 얻어내기 위함이다.
매질의 특성이라 함은 $mu_a$,  $mu_s'$을 의미한다.
하지만 빛을 쏴 얻을 수 있는건 amp와 phase 밖에 없다.



처음에 구할땐 취득한 데이터를 토대로
curve fitting
non-linear상태에서 해당 주어진 output을 가지고 가장 근접한 input을 찾는것.
# CW
- 초기에 알고 있는 값.
	- Reference phantom data : $\mu_a$, $\mu_s'$
	- Measured phantom data : Amp1, Amp2, Amp3
- 측정해서 나온 값
	- Target data(Amp1,Amp2,Amp3)

## CW normalization 
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

light source를 50Mhz - 500Mhz modulation을 걸어 target에 쏜다.
p는 고정 
처음엔 무조건 calibration 과정이 필요함
준비물 : Reference phantom (인체와 유사한 $\mu_a$, $\mu_s'$를 지닌 물질)
애시당초에 phantom을 만들때 $\mu_a$, $\mu_s'$을 넣어주니까 알고있음.
처음에는 Target이 phantom이다.
빛을 쏘면 Amp와 phase를 알수 있는데,
p1approximation을 통해 amp를 구한다. 
amp는 나눠주고 phase는 빼주고

input : $\mu_a$, $\mu_s'$, $f$ (modulation frequency)
model : p1 Approximation
output : AMp phase

## 실제 데이터
Target에 빛을 쐈을때 얻은 Amp와 phase를
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
eyJoaXN0b3J5IjpbNTkzMTk2Nzg1LC04MTA3NTY4NDQsLTc0NT
IzNDI2OSwtOTA3NjU1MjgxLDc0MjY3NDM0NSwyOTUzMDA3Njcs
MTczNTEzOTU4MCwtOTQ4MjE5ODRdfQ==
-->