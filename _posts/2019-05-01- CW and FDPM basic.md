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
## FDPM nomalization
CW와 다른점이 얘는 Amp와 phase가 다르다
- Amplitude
기존에 알고
- Phase

p1seminf을 통
n이 frequency 
여기는 빼는것.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTM3OTQ4Nzg2MCwtOTA3NjU1MjgxLDc0Mj
Y3NDM0NSwyOTUzMDA3NjcsMTczNTEzOTU4MCwtOTQ4MjE5ODRd
fQ==
-->