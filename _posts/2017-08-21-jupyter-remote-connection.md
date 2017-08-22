---
title: 'About Jupyter'
date: '2017-8-21 10:00'
layout: post
published: true
---

Jupyter를 사용해 보자.

### Connect Jupyter from remote machine 

원격지의 컴퓨터에서 실행되는 주피터 서버에 접속할 필요가 있을 것이다. 이 경우, 서버 측에서는 다음과 같이 `--no-browser` 옵션을 주어서 실행한다:
```
jupyter notebook --no-browser --port=[XXXX]
```

로컬 컴퓨터에서는, 다음과 같이 실행하여 jupyter 서버와 로컬 컴퓨터간의 ssh 터널을 생성한다. 그러면, 로컬 컴퓨터에서 locahost address를 이용하여 서버에 접속할 수 있게 된다. 
```
ssh -f [USER]@[SERVER] -L [YYYY]:localhost:[XXXX] -N
```

다음의 주소를 브라우저에 입력하여 Jupyter 서버에 접속해 보자. 
```
localhost:[YYYY] 
```

[여기](https://coderwall.com/p/y1rwfw/jupyter-notebook-on-remote-server)에서 더 자세한 내용을 볼 수 있다. 

참고사항 

[Jupyter R kernel](https://github.com/IRkernel/IRkernel)

[Jupyter Theme](https://github.com/dunovank/jupyter-themes)
