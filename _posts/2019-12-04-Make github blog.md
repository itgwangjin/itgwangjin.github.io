---
title: "Make own github blog"
collection: post
permalink: /posts/2019/12/Make own github blog
date: 2019-12-05
tag:
  - blog
---
# 자신만의  블로그를 만들어보자

Pipeline
1. Jekyll [Theme](https://jekyllthemes.io/)를 Clone
2. 내 입맛에 맞게 수정
	- posts 폴더 만들기 
	-  profile 수정
	_config.yml 파일 수정
	-  menu 수정
	navigation.yml 수정
		- About : 짧은 내 설명
		- CV : 나의 CV
		- Publications : 논문발행건,
		- (주석)Teaching : 가르친경험
		- [Tag] : Tag별로 모아놓은것.
		- Categories : Categories별로 모아 놓은것.
3.  기능 추가
	- [LaTex 기능 추가](https://blog.naver.com/PostView.nhn?blogId=prt1004dms&logNo=221525385428&parentCategoryNo=&categoryNo=&viewDate=&isShowPopularPosts=false&from=postView)

4. 알면 유용한 기능
	- 에디터
		- Stackedit.
		- Brackets.
	- [화면 .gif 파일로 녹화](https://gocoder.tistory.com/338)
	
## 1. Jekyll Theme
1. Clone할 Theme [링크](https://github.com/gwangjinjeong/academicpages.github.io)에 들어가서 내 계정으로 로그인 하고 Fork 해준다.
2. 간편한 코드 수정을 위해서 Github Desktop을 통해서 내 계정에 있는 Repository를 동기화 시켜준다.

## 2. 입맛에 맞게 수정

### 1. 개인정보 수정
_config.yml 파일 수정
#### (1) tl
```markdown
# Site Settings
locale                   : "en-US"
title                    : "Jerry(Gwangjin) Jeong"
title_separator          : "-"
subtitle                 : # site tagline that appears below site title in masthead
name                     : "Gwangjin jeong"
description              : "Deep learning, Biomedical engineer"
url                      : "https://gwangjinjeong@github.io"
```
#### (2) profile & logo image 추가
assets/image 폴더에 파일 추가
 

### 2. 목차 수정
_data/navigation.yml
- About : 짧은 내 설명
- CV : 나의 CV
- Publications : 논문발행건,
- (주석)Teaching : 가르친경험
- [Tag] : Tag별로 모아놓은것.
- Categories : Categories별로 모
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTE4OTc4NDE1MTAsNDk3NDM3NzIzLDY4Mj
kxNTc1OCwtMTE1MzExNjA1OCwyMDQwNTA3ODU2LC03MTQ0OTQx
MTYsMTM4NTAyODIzMiwyMDI5ODEyODY5LDEzMzE5MzAyNzcsNj
cxMDU3MTQyLC0xMTg1NDAzMTU2LC04ODc4ODE1MjhdfQ==
-->