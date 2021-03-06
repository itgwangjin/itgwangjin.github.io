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
 ```markdown
teaser                   : "/assets/images/profile.png"
logo                     : "/assets/images/logo.png"
```
#### (3) 신상정보 추가
```markdown
# Site Author
author:
  name             : "Jerry(Gwangjin) Jeong"
  avatar           : "/assets/images/profile.png"
  bio              : "Deep learning & biomedical engineer."
  location         : "South Korea"
#  email            : 
  links:
    - label: "Email"
      icon: "fas fa-fw fa-envelope-square"
      url: mailto:ai.gwangjin@gmail.com
#    - label: "Website"
#      icon: "fas fa-fw fa-link"
#      # url: "https://your-website.com"
#    - label: "Twitter"
#      icon: "fab fa-fw fa-twitter-square"
#      # url: "https://twitter.com/"
#    - label: "Facebook"
#      icon: "fab fa-fw fa-facebook-square"
#      # url: "https://facebook.com/"
    - label: "GitHub"
      icon: "fab fa-fw fa-github"
      url: "https://github.com/gwangjinjeong"
#    - label: "Instagram"
#      icon: "fab fa-fw fa-instagram"
#      # url: "https://instagram.com/"
#    - label: "linkedin"
#      url: ""
#    - label: "googlescholar"
#      url: ""
#    - label: "researchgate"
#      url: ""
#    - label: "stackoverflow"
#      url: ""
```

#### (4) 블로그 메인 뷰 및 시간 설정
```markdown
# Outputting
permalink: /:categories/:title/
paginate: 5 # amount of posts to show
paginate_path: /page:num/
timezone: Asia/Seoul 
```

### 2. 목차 수정
#### (1) About : 짧은 내 설명

##### 1) _data/navigation.yml
```markdown
main:
- title: "About"
  url: /about/
```
#####  2)_page/about.md추가
	
	
```markdown
	---
	title: "Gwangjin jeong"
	permalink: /about/
	layout: single
	---

	# In Essence, I…   
	---
	Am a Deep learning & biomedical engineer.

	Received my bachelor’s degree in computer science.

	Am a biomedical master student.

	Am Interested to find biomarkers using deep learning.

	Am Interested in Diffuse optics.

	Want to contribute to the development of future diagnostic technology
```
#### (2) CV : 나의 CV
##### 1) _data/navigation.yml
```markdown
main:
- title: "CV"
  url: /cv/
```
##### 2)_page/cv.md
```markdown
---
title: "CV"
layout: single
permalink: /cv/
author_profile: true
---

Education
======
* B.S. in GitHub, GitHub University, 2012
* M.S. in Jekyll, GitHub University, 2014
* Ph.D in Version Control Theory, GitHub University, 2018 (expected)

Work experience
======
* Summer 2015: Research Assistant
  * Github University
  * Duties included: Tagging issues
  * Supervisor: Professor Git

* Fall 2015: Research Assistant
  * Github University
  * Duties included: Merging pull requests
  * Supervisor: Professor Hub
  
Skills
======
* Skill 1
* Skill 2
  * Sub-skill 2.1
  * Sub-skill 2.2
  * Sub-skill 2.3
* Skill 3

<!-- 추
Publications
======
  <ul>{% for post in site.publications %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
Talks
======
  <ul>{% for post in site.talks %}
    {% include archive-single-talk-cv.html %}
  {% endfor %}</ul>
  
Teaching
======
  <ul>{% for post in site.teaching %}
    {% include archive-single-cv.html %}
  {% endfor %}</ul>
  
Service and leadership
======
* Currently signed in to 43 different slack teams
-->

```


#### (3) Publications : 논문발행건,
##### 1) _data/navigation.yml
```markdown
main:
- title: "CV"
  url: /cv/
```
##### 2)_page/cv.md
```markdown

```
#### (주석) Teaching : 가르친경험
##### 1) _data/navigation.yml
##### 2)_page/cv.md

### (4) Tag : Tag별로 모아놓은것.
##### 1) _data/navigation.yml
```markdown
  - title: "Tags"
    url: /tags/
```
##### 2)_page/tag-archive.md
```markdown
---
title: "Posts by Tag"
permalink: /tags/
layout: tags
author_profile: true
---
```
#### (5) Categories : Categories별로 모
##### 1) _data/navigation.yml
```markdown
  - title: "Categories"
    url: /categories/
```
##### 2)_page/category-archive.md
```markdown
---
title: "Posts by Category"
layout: categories
permalink: /categories/
author_profile: true
---
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbLTg2NDMzNjU2NSwtNzI5Mjk1NjAsMTQxNj
A5MTEzMCw0OTc0Mzc3MjMsNjgyOTE1NzU4LC0xMTUzMTE2MDU4
LDIwNDA1MDc4NTYsLTcxNDQ5NDExNiwxMzg1MDI4MjMyLDIwMj
k4MTI4NjksMTMzMTkzMDI3Nyw2NzEwNTcxNDIsLTExODU0MDMx
NTYsLTg4Nzg4MTUyOF19
-->