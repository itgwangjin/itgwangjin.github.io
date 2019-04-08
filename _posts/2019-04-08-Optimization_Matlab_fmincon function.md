---
title: "Optimization_Matlab_fmincon function"
collection: post
permalink: /posts/2019/04/Optimization_Matlab_fmincon function
date: 2019-04-08
tag:
  - Matlab
  - fmincon
  - Optimization
---

# 1. Non-linear Optimization 
## (1)  fminsearch function
#### 1) 구문
##### x = fminsearch(fun,x0)
점 x0에서 시작해서 fun에 정의된 함수의 최솟값x를 구한다.
##### x = fminsearch(fun,x0,options)

구조체 **options**에 지정된 최적화 옵션을 사용하여 최소화한다.
- optimset
최적의 options 구조체를 만들거나 편집할 수 있다.
	- 예제
``` matlab
options = optimset('Display','iter','TolX',1e-8) % display 옵션이 iter, Tolx옵션이 1e-8
optnew = optimset(options,'TolX',1e-4); % TolX옵션의 값을 변경하고 새 값을 optnew에 새 값 저장하고 options라는 options 구조체의 복사본을 만든다.
options = optimset('fminbnd') % fminbnd와 관련된 모든 옵션 이름과 디폴트 값을 포함하는 optimization options 구조체 options 반환
optimset fminbnd % 디폴트 값만 볼때
```
	
##### x = fminsearch(problem)
구조체 problem의 최솟값을 구한다.
##### [x,fval] = fminsearch(___)
모든 입력 구문에 대해 fun의 최솟값을 fval로 반환, x에는 해가 되는 위치 값을 반환
##### [x,fval,exitflag] = fminsearch(___)
종료 상황을 설명하는 값 exitflag를 추가로 반환
##### [x,fval,exitflag,output] = fminsearch(___)
최적화 과정에 대한 정보가 포함된 구조체 output을 추가로 반환

예제
``` matlab
options = optimset('PlotFcns',@optimplotfval); % 목적함수 = PlotFcns
fun = @(x)100*(x(2) - x(1)^2)^2 + (1 - x(1))^2; % 로젠브룩 함수
x0 = [-1.2,1]; % 시작점
x = fminsearch(fun,x0,options) % 로젠브룩 함수를 통해 시작점 x0의 최솟값을 구한다.
```

> Nearest search를 썼을때 Euclidean distance 함수를 쓴것으로 보아
 matlab에서  fun  = @(x)sqrt(sum((x(1) - x(2))^ 2)); 을 쓰는 것이 맞지않나싶다 

## 2) 제약조건이 있는 최적화 - fmincon function
### (1) 정의
비선형 다변수 함수의 최솟값을 찾는 함수입니다.

![enter image description here](https://lh3.googleusercontent.com/3Im8xS2vCpiTIMEdCylQUVgWdqKDiZkBSs7XQV4BSjjZfSj3M7fqqYMirqQqCj8xIkeygxy5gA0 "fmincon")

위와 같은 문제의 최솟값을 구합니다.


### (2) 구문
기본적으로 이 함수를 구현해야할 때는 크게 2가지는 기억하고 있어야한다.

**첫째로**. 어떤 함수를 최소화시키고 싶은지(objective function)
**둘째로**. 최소화된 값이 적어도 어느 범위안에 있어야 하는지? (Constraints)

### Example
Objective function : Rosenbrock function
$$ f(x) = 100(x_2 - x_1^2)^2 + (1 - x_1)^2$$

#### 첫번째  Example
Constraints : $A*x ≤ b$
``` matlab
x = fmincon(fun,x0,A,b)
```

정의 : x0에서 시작하여 fun에 정의된 함수의 최소점을 찾는다.
- Constraints : $x_1 + 2x_2 \le 1$
``` matlab
x0 = [-1,2];
A = [1,2];
b = 1;
x = fmincon(fun,x0,A,b)
```
예를 들어 $x_1^2 + x_2^2 \le 1$ 와 같은 부등식 제약조건도 의미한다.

#### 두번째 Example
Constraints : 제약조건이 2개(선형 부등식, 등식 제약 조건)
``` matlab
x = fmincon(fun,x0,A,b,Aeq,beq)
```
정의 : $Aeq*x = beq$ 및 $A*x ≤ b$이 적용되어 fun을 최소점을 찾는다.

- Constraints 1 : $x_1 + 2x_2 \le 1$ 
- Constraints 2 : $2x_1 + x_2 = 1$
``` matlab
x0 = [0.5,0];
A = [1,2];
b = 1;
Aeq = [2,1];
beq = 1;
x = fmincon(fun,x0,A,b,Aeq,beq)
```
(부등식이 존재하지 않는 경우 A = [] 및 b = []로 설정)


####  세번째 Example
- Objective fucntion : ${{1+x_1} \over {1+x_2}} - 3x_1x_2 + x_2(1+x_1)$
- Constraints : $lb ≤ x ≤ ub$ 
``` matlab
x = fmincon(fun,x0,A,b,Aeq,beq,lb,ub)
```
정의 : 해가 항상 범위 제약조건 내에 있도록 x의 설계 변수에 대한 하한 및 상한 집합정의
Constraints 1 : $0 \le x_1\le 1$ 
Constraints 2 : $0 \le x_2 \le 2$
``` matlab
lb = [0,0];
ub = [1,2];
% 선형제약 조건이 없으므로 A, b, Aeq, beq는 공백으로
A = [];
b = [];
Aeq = [];
beq = [];
```
등식이 존재하지 않는 경우 Aeq = [] 및 beq = []을 설정하십시오. 

#### 네번째 Example
- Objective fucntion : $f(x) = 100(x_2 - x_1^2)^2 + (1 - x_1)^2$
- Constraints 1 : $0 \le x_1\le 0.5$ 
- Constraints 2 : $0.2 \le x_2 \le 0.8$
- Constraints 3 : $(x_1 - {1 \over 3}) ^2 +(x_2 - {1 \over 3}) ^2  -({1 \over 3})^2$
						=> 원 내부
``` matlab
x = fmincon(fun,x0,A,b,Aeq,beq,lb,ub,nonlcon)
```
정의 : 비선형 제약 조건을 적용하여 함수의 최솟값을 구합니다.
``` matlab
function [c,ceq] = circlecon(x)
c = (x(1)-1/3)^2 + (x(2)-1/3)^2 - (1/3)^2;
ceq = [];
```

``` matlab
lb = [0,0.2];
ub = [0.5,0.8];
% 선형조건이 없으므로
A = [];
b = [];
Aeq = [];
beq = [];
% 초기값 설정
x0 = [1/4,1/4];
% 실행
nonlcon = @circlecon;
x = fmincon(fun,x0,A,b,Aeq,beq,lb,ub,nonlcon)
```

#### 다섯번째 Example 
- Objective function : 
``` matlab
x = fmincon(fun,x0,A,b,Aeq,beq,lb,ub,nonlcon,options)
```
정의 : 더욱 빠르거나 더욱 안정적인 계산을 위해 목적 함수에 기울기 계산을 포함시킵니다. 목적 함수 파일에 조건화된 출력값으로 기울기 계산을 포함

``` matlab
function [f,g] = rosenbrockwithgrad(x)
% Calculate objective f
f = 100*(x(2) - x(1)^2)^2 + (1-x(1))^2;

if nargout > 1 % gradient required
    g = [-400*(x(2)-x(1)^2)*x(1)-2*(1-x(1));
        200*(x(2)-x(1)^2)];
end
```
옵션을 줌으로써 objective function의 기울기를 사용하도록 만든다.
``` matlab
options = optimoptions('fmincon','SpecifyObjectiveGradient',true);
```
그밖의 입력값 
``` matlab
fun = @rosenbrockwithgrad;
x0 = [-1,2];
A = [];
b = [];
Aeq = [];
beq = [];
lb = [-2,-2];
ub = [2,2];
nonlcon = [];
x = fmincon(fun,x0,A,b,Aeq,beq,lb,ub,nonlcon,options)
```

#### 마지막 example
Objective function : 
Constraints : 
`fmincon`은 보고된 해를 분석하는 데 사용할 수 있는 여러 출력값을 선택적으로 반환합니다.
``` matlab
function [c,ceq] = unitdisk(x)
c = x(1)^2 + x(2)^2 - 1;
ceq = [];
---------------------------------
fun = @(x)100*(x(2)-x(1)^2)^2 + (1-x(1))^2;
nonlcon = @unitdisk;
A = [];
b = [];
Aeq = [];
beq = [];
lb = [];
ub = [];
x0 = [0,0];
---------------------------
[x,fval,exitflag,output,lambda,grad,hessian] = fmincon(fun,x0,A,b,Aeq,beq,lb,ub,nonlcon)
```

출력값
```
x = 0.7864    0.6177
fval = 0.0457
exitflag = 1
output = struct with fields:
         iterations: 24
          funcCount: 84
    constrviolation: 0
           stepsize: 6.9162e-06
          algorithm: 'interior-point'
      firstorderopt: 2.4373e-08
       cgiterations: 4
            message: 'Local minimum found that satisfies the constraints....'
lambda =  struct with fields:
         eqlin: [0x1 double]
      eqnonlin: [0x1 double]
       ineqlin: [0x1 double]
         lower: [2x1 double]
         upper: [2x1 double]
    ineqnonlin: 0.1215
grad =
   -0.1911
   -0.1501
hessian =
  497.2903 -314.5589
 -314.5589  200.2392
```
**결과값 분석**
- x
- fval
- exitflag
![|center| 300x0](https://lh3.googleusercontent.com/JCmvURDDduT3VDSIkNvc9ZHOQtP2m7YCNAEIe5xdLr6-q_u74JaaxRhZoOqXUoidtzU-d6BNa0E "exitflag")
- output 
![
](https://lh3.googleusercontent.com/dtqc9-iNFT0BzMFd23oQ4i3Ws4kuk0gHQDd_s1w1k7iScLDVTLDUJnkEzoAZHrx_tzP-gpy_M_lU "output")
`lambda.ineqnonlin` 출력값은 비선형 제약 조건이 해에서 활성 상태라는 것을 보여주고 연결된 라그랑주 승수의 값을 제공

grad —  x에서의 fun의 기울기입니다.

hessian —  x에서의 fun의 hessian matrix입니다. fmincon Hessian 항목을 참조하십시오.

---

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEzMzg0MTM2MDksLTE1NDY1MzUzMTIsMT
c3MzgwMjMwOF19
-->