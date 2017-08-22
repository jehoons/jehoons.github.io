---
title: 'About Jupyter'
date: '2017-8-21 10:00'
layout: post
published: true
---

Jupyter를 사용해 보자.

### Connect Jupyter from remote machine 

서버 측에서는 다음 명령을 이용하여 실행한다:
```
jupyter notebook --no-browser --port=[XXXX]
```

로컬 컴퓨터에서는 다음 명령을 이용하여, Jupyter 서버에 대한 ssh 터널 생성 및 원격의 포트 XXXX를 로컬 포트 YYYY로 바인딩한다: 
```
ssh -f [USER]@[SERVER] -L [YYYY]:localhost:[XXXX] -N
```

아래의 주소를 브라우저에 입력하여 Jupyter 서버에 접속할수 있다. 
```
localhost:[YYYY] 
```

[여기](https://coderwall.com/p/y1rwfw/jupyter-notebook-on-remote-server)에서 더 자세한 내용을 볼 수 있다. 

### Jupyter R kernel 

내용은 [여기](https://github.com/IRkernel/IRkernel) 참고 

### Jupyter Theme

내용은 [여기](https://github.com/dunovank/jupyter-themes) 참고 
