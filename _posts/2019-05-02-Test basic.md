---
title: "Test basic"
collection: post
permalink: /posts/2019/05/Test basic
date: 2019-05-02
tag:
  - A/B TEST
  - Hypothesis
  - Critical Value alpha
  - t-test
  - p-value
  - p-hacking

---

Data science와 statistics에서는 빠지지 않고 나오는 이야기
A/B TEST, Hypothesis, Critical Value alpha, t-test, p-value, p-hacking에 대해서 알아보도록 하겠습니다.

Content
1. A/B TEST란?
2. Hypothesis?
3. Critical Value alpha($\alpha$) ?
4. t-test
5. p-value
6. p-hacking

# 1. What is A/B Test
## 의미
1. 시스템 방문자를 임의로 두 집단으로 나눈다.
2. 한 집단에게는 기존 사이트를 보여준다
3. 다른 집단에게는 새로운 사이트를 보여준다.
4. 두 집단 중 어떠한 집단이 더 높은 만족을 나타내는지 측정하여, 정량적으로 평가한다.

## 목적
복수의 상황에 대한 고객 반응을 테스트하여 최적의 방안을 식별한다.

## 사례
오바마 캠프
![](http://mindthelog.com/wp-content/uploads/2017/01/a-b-testing.jpg)
와 같이 실제로 투표율을 높임으로써 현실세계에서
잘 쓰이는 기법 중 하나

## So.. what is A/B test
A = B 이느냐를 확인함으로써
`차이가 있다/없다`를 계속 상황을 변경시키는 것을 의미

# 2. Hypothesis
앞에서 보았던 A/B test에서
`차이가 있다/없다`를 본다는 것임을 일수 있다.
여기서 A의 영향을 $p_A$, B의 영향을 $p_B$라고 하고,
 null hypothesis(귀무가설)을 $H_o$ ,
 alternative hypothesis(대립가설)을 $H_1$이라고 한다면,
>$H_0 : d = p_A - p_B = 0$
>$H_1 : d = p_A - p_B  >0$

위와 같이 차이가 없다를 null hypothesis 차이가 조금이라도 있다를 alternative hypothesis이라고 한다.
## Type I & II Error
![](http://epiville.ccnmtl.columbia.edu/assets/images/error_table.jpg)
-   Type I Error: 1종 오류, 귀무가설이 사실인데 기각할 오류 
=> 즉 효과가 없는데 있다고 할 오류
-   Type II Error: 2종 오류, 귀무가설이 거짓인데 기각하지 않을 오류
=> 효과가 있는데 없다고 할 오류

# 3. 임계치(Critical Value alpha)
현실세계에서 Type I Error 와 Type II Error 중에서 어느쪽에 무게를 더 실을지를 정해야한다.

<참고 blog>
[http://blog.naver.com/PostView.nhn?blogId=leerider&logNo=100189538379&parentCategoryNo=&categoryNo=59&viewDate=&isShowPopularPosts=true&from=search](http://blog.naver.com/PostView.nhn?blogId=leerider&logNo=100189538379&parentCategoryNo=&categoryNo=59&viewDate=&isShowPopularPosts=true&from=search)

[https://boxnwhis.kr/2016/04/15/dont_be_overwhelmed_by_pvalue.html](https://boxnwhis.kr/2016/04/15/dont_be_overwhelmed_by_pvalue.html)
<!--stackedit_data:
eyJoaXN0b3J5IjpbMTc5MTIwODAzMSwtMTA0MzA2Mzg1NSwxNT
AwNjQyNjcxLC00ODUyNTE1NzAsLTQ4ODE3OTY5NiwtMTE5MDMy
MTEwXX0=
-->