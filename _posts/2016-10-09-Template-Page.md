---
layout: post
title: Template Page
date: '2016.10.09 19:00'
published: true
---
블로그 페이지를 만들기 위한 기본 골격

### 수학식작성 
When $a \ne 0$, there are two solutions to $ax^2 + bx + c = 0$ and they are 

$$x = {-b \pm \sqrt{b^2-4ac} \over 2a}.$$

TEX사용법은 [TEX WIKI](https://en.wikibooks.org/wiki/LaTeX/Mathematics)참고

### 소스코드넣기
 
```python 
import os,sys,pandas 
sys.path.append('.') 
print 'hello'
```

### 이미지넣기
여기서는 구글포토에서 이미지를 넣는다.

* [photos.google.com](https://photos.google.com/u/1/)
* 이미지 업로드
* 이미지 선택후 마우스 우측클릭하여 이미지 주소를 복사 
* 주소가 긴 경우는 [goo.gl](https://goo.gl/)에 접속하여 짧은 주소 생성

![alt text](https://goo.gl/J6vin1 "this is image")

