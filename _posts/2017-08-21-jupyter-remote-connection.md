---
title: 'Jupyter remote connection'
date: '2017-8-21 10:00'
layout: post
published: true
---

Jupyter를 원격 컴퓨터에서 접속하기. 

*리모트 서버 설정*
```
jupyter notebook --no-browser --port=[XXXX]
```

*로컬 컴퓨터 설정*
Jupyter 서버에 대한 ssh 터널 생성 및 원격의 포트 XXXX를 로컬 포트 YYYY로 바인딩하기:
```
ssh -f [USER]@[SERVER] -L [YYYY]:localhost:[XXXX] -N
```

*로컬 컴퓨터 브라우저에서 접속하기*
```
localhost:[YYYY] 
```