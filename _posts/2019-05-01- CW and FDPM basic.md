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
	- Reference_optical property : $\mu_a$, $\mu_s'$
- 측정해서 나온 값
	- Target data
	- Measured data(Amp1,Amp2,Amp3)

## CW normalization 
system response를 없애주는 과정
### 1.System response를 구한다.
\* **system response?** -> 기기의 고유 특성
> Measured Amp    
> Theoretical R   

이 두개를 나눠줌으로써 system response를 구한다.

### 2. 
Target Amp을 system response를 내려서 
Target Reflectance를 구할 수 있다. (R1, R2, R3)
이를 least square curve fit을 통해서


<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE0MjA5NDUyMTUsNzQyNjc0MzQ1LDI5NT
MwMDc2NywxNzM1MTM5NTgwLC05NDgyMTk4NF19
-->