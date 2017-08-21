---
title: 'About Jupyter'
date: '2017-8-21 10:00'
layout: post
published: true
---
Jupyter 사용하기 

### Jupyter를 원격 컴퓨터에서 접속하기 

**1. 리모트 서버 설정**

```
jupyter notebook --no-browser --port=[XXXX]
```

**2. 로컬 컴퓨터 설정**

Jupyter 서버에 대한 ssh 터널 생성 및 원격의 포트 XXXX를 로컬 포트 YYYY로 바인딩하기:
```
ssh -f [USER]@[SERVER] -L [YYYY]:localhost:[XXXX] -N
```

**3. 로컬 컴퓨터 브라우저에서 접속하기**

아래의 주소를 브라우저에 입력하여 Jupyter 서버에 접속할수 있다. 
```
localhost:[YYYY] 
```

> 이 내용 원본은 [여기](https://coderwall.com/p/y1rwfw/jupyter-notebook-on-remote-server)에서 발췌한 것입니다. 


