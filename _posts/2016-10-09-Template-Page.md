---
title: Template Page
date: 2016-10-09 19:00:00 Z
published: false
layout: post
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
여기서는 [구글포토](https://photos.google.com/u/1/)를 이용하여 이미지를 업로드한다. 업로드 후에는 이미지를 선택 후 마우스의 우측버튼을 클릭하여 이미지 주소를 복사하자. 보통 이미지의 주소가 매우 길다. 그러면, [goo.gl](https://goo.gl/)에 접속하여 짧은 주소를 생성하여 넣으면 된다.

![alt text](https://goo.gl/J6vin1 "this is image")
