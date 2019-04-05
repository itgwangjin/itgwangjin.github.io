---
title: "Optimization - Nelder Mead simplex algorithm"
collection: post
permalink: /posts/2019/04/Optimization - Nelder Mead simplex algorithm
date: 2019-04-04
tag:
  - Deeplearning
  - Optimization
  - Nelder-Mead simplex
---

# Nelder-Mead simplex optimization algorithm

## 0. Introduction
Matlab fminsearch함수는 [Nelder-Mead simplex algorithm](http://www.scholarpedia.org/article/Nelder-Mead_algorithm)을 사용한다.
변수가 여러개인 미분 불가능한  함수에서 최소 값을 찾는 방법이다.

# 1. Run flow
![Nelder-Mead Simplex search example](https://miniopt.files.wordpress.com/2015/01/nelder_mead2.gif?w=660)

## 초기 simplex
- N차원 공간에서 $N+1$개의 꼭짓점을 갖는 다각형을 만든다.
- input point : $x_0, ... , x_n$
- the most frequenct choice is $x_0 = x_{input}$
- 나머지 n 개의 꼭지점을 생성하여 S의 두 표준 모양 중 하나를 얻습니다

## Simplex transformation algorithm
Nelder-Mead method consists of the following three steps.
### 1. Ordering : Determine the indices $h,s,l$ of worst, second worst and the best vertex.
$f_h = max_jf_j$, $f_s = max_{j \ne h}f_j$, $f_l = min_{j \ne h} f_j$
S의 vertices를 모두 크기순으로 정렬한다. $ f(x_0) \le f(x_2) \le ... \le f(x_{N})$ 
그러면 l=0, s= n-1, h=n이 될것이다.
### 2. Centroid : 가장 큰  $x_{n+1}$를 제외하고 모든 점의 중심인 $x_c$를 계산 한다,
### 3. Transformation : 
First, try to replace only the worst vertex $x_{n+1}$ with a better point by using reflection,
expansion or contraction with respect to the best side.
$x_r$  := $x_c +\alpha(x_c-x_{N+1})$ , $\alpha>0$를 계산한다.
### 4. 이제 3가지의 경우로 나뉘는데,
 
 
#### **4-1. Reflection**
$f(x_1) \le f(x_r) \le f(x_N) $일 경우
![Reflection|center|300x0](http://www.scholarpedia.org/w/images/d/d4/NelderMead_1.jpg)
#### **4-2. Expansion**
$f(x_r) \le f(x_l) $일 경우 = 구한 새로운 값이 최소값보다 작을 경우
![Contraction|center|300x0](https://codesachin.files.wordpress.com/2016/01/neldermead_2.jpg?w=214&h=122)

####  **4-3. Contraction**
![c1](http://www.scholarpedia.org/w/images/6/65/NelderMead_4.jpg) ![c2](http://www.scholarpedia.org/w/images/8/84/NelderMead_3.jpg)

장점 : 항상 convergence가 된다.
단점 : iteration을 많이 돌아야 하고 3개의 control parameter를 찾아야하는 단점이 있다.

참고 블로그 : [link](http://www.scholarpedia.org/article/Nelder-Mead_algorithm)

