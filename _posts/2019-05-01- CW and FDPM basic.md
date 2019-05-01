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

phase

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
우리가 알고 싶은건 매질의 특성 mua mus인거고
우리가 얻을 수 있는건 amp나 ref data밖에 없음
매질의 특성을 알기 위한건 mua mus

처음에 구할땐 취득한 데이터를 토대로
curve fitting
non-linear상태에서 해당 주어진 output을 가지고 가장 근접한 input을 찾는것.
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTk2MzQzMjM0MiwtNzQ1MjM0MjY5LC05MD
c2NTUyODEsNzQyNjc0MzQ1LDI5NTMwMDc2NywxNzM1MTM5NTgw
LC05NDgyMTk4NF19
-->