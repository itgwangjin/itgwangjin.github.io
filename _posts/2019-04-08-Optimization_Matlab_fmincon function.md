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
Objective fucntion : ${{1+x_1} \over {1+x_2}} - 3x_1x_2 + x_2(1+x_1)$
Constraints : $lb ≤ x ≤ ub$ 
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
Objective fucntion : $f(x) = 100(x_2 - x_1^2)^2 + (1 - x_1)^2$
$Constraints 1 : $0 \le x_1\le 0.5$ 
Constraints 2 : $0.2 \le x_2 \le 0.8$
``` matlab
x = fmincon(fun,x0,A,b,Aeq,beq,lb,ub,nonlcon)
```

은 nonlcon에 정의된 비선형 부등식 c(x) 또는 등식 ceq(x)를 최소화에 적용합니다. fmincon은 c(x) ≤ 0 및 ceq(x) = 0 조건에서 최적화합니다. 범위가 존재하지 않는 경우 lb = [] 및/또는 ub = []을 설정하십시오

######x = fmincon(fun,x0,A,b,Aeq,beq,lb,ub,nonlcon,options)
는 options에 지정된 최적화 옵션을 사용하여 최솟값을 구합니다. 이 옵션을 설정하려면 optimoptions를 사용하십시오. 비선형 부등식 또는 등식 제약 조건이 없을 경우 nonlcon = []을 설정하십시오.
######x = fmincon(problem)
은 problem의 최솟값을 구합니다. 여기서 problem은 구조체(입력 인수에 설명되어 있음)입니다. problem 구조체는 작업 내보내기에 설명된 대로 최적화 앱에서 문제를 내보내어 만들 수 있습니다.
######[x,fval] = fmincon(___)

######[x,fval,exitflag,output,lambda,grad,hessian] = fmincon(___)
 fmincon(___)은 추가로 다음을 반환합니다.

lambda — 해 x에서의 라그랑주 승수를 포함하는 필드를 갖는 구조체입니다.

grad — 해 x에서의 fun의 기울기입니다.

hessian — 해 x에서의 fun의 헤세 행렬입니다. fmincon Hessian 항목을 참조하십시오.

---

# 최적화를 실행시켜주는 UI Optimtool
## objective function

## non-linear function


## 결과 해석
![Alt text](./1554708465452.png)

- Iter는  반복 횟수입니다. fmincon은 수렴하기까지 24회의 반복을 거쳤습니다.

- F-count라는 레이블이 지정된 두 번째 열은 로젠브록 함수가 실행된 누적 횟수를 보고합니다. 마지막 행은 F-count가 84임을 보여주며, 이는 fmincon이 최솟값을 구하는 과정에서 로젠브록 함수를 84회 실행했음을 나타냅니다.

- f(x)라는 레이블이 지정된 세 번째 열은 목적 함수의 값을 표시합니다. 최종 값 0.04567482는 최적화 앱의 솔버 실행 및 결과 보기 상자에서 보고된 최솟값이며 명령 창의 종료 메시지 끝에 있습니다.

- Feasibility는 모든 반복에 대해 0입니다. 이 열은 제약 조건이 양수인 각 반복에서 제약 조건 함수 unitdisk의 값을 보여줍니다. unitdisk의 값이 모든 반복에서 음수였기 때문에 매 반복마다 제약 조건을 충족했습니다.

<!--stackedit_data:
eyJoaXN0b3J5IjpbLTEyMDYyNTQ2NjNdfQ==
-->