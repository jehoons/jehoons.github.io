---
title: 'How to make JAR file executable in linux'
date: '2017-4-15 10:00'
layout: post
published: true
---

JAR(Java ARchive)는 여러 자바클레스 파일, 연관된 메타데이터, 텍스트/이미지 등의 리소스 파일들을 하나의 파일안으로 모아놓기 위해서 전형적으로 사용하는 일종의 패키지 파일형식입니다. JAR파일로 패키징을 하는 중요한 목적은 자바플랫폼에서 실행되는 응용프로그램의 라이브러리를 배포하기 위해서입니다. JAR파일은 근본적으로 아카이브 파일들인데, ZIP파일의 형식 및 .jar파일 확장자를 가질 수 있습니다. 여기서, 그러한 JAR파일을 실행가능한 형태의 파일로 변환하는 방법에 대해서 설명합니다. 

유저는 jar명령어로 JAR파일을 생성하거나 그 안의 내용물들을 추출할 수 있습니다. zip 프로그램 도구를 이용해서 같은 일을 할 수도 있지요. 하지만, 압축할때 zip파일 헤더안에 있는 엔트리의 순서는 압축시 중요한데, 그 이유는 (내용물에 관한) 목록이 첫번째가 되어야 할 필요가 있기 때문입니다. JAR파일내에서 파일의 이름들은 유니코드 텍스트입니다.

우선 다음 자바소스코드, `HelloWorld.java`가 있다고 가정합니다.

```java
/* HelloWorld.java */
public class HelloWorld {
    public static void main(String[] args) {
        System.out.println("Hello, World");
    }
}
```

`HelloWorld.java`는 아래의 명령어를 이용하여 컴파일합니다.

```
$ javac HelloWorld.java 
```

그러면 `HelloWorld.jar`파일이 생성되는데 실행하는 방법은 다음과 같습니다:

```bash 
$ java –jar HelloWorld.jar
```

그러면 `HelloWorld.class` 파일이 컴파일되어서 생성됩니다. 클레스 안에는 메인함수가 포함됩니다. 이 클래스를 .jar파일에 추가하고 이 클래스가 실행되도록 하려면 `MANIFEST.MF`파일을 jar 패키지에 추가해야 합니다. 이 파일은 개발한 어플리케이션의 메인메소드가 정의된 클레스가 무엇인지 기술하는 `Main-Class` 엔트리가 반드시 포함되어야 합니다.

예를 들면 다음과 같습니다:

```bash
$ javac HelloWorld.java
$ echo Main-Class: HelloWorld > MANIFEST.MF
$ jar -cvmf MANIFEST.MF HelloWorld.jar HelloWorld.class
```

여기서 생성되어진 jar 패키지 파일은 다음 명령을 이용하여 실행할 수 있습니다.

```bash
$ java –jar HelloWorld.jar 
```

하지만, 여기서 `java –jar`이 여전히 함께 사용되어야 합니다. 이것을 없애기 위해서는 어떻게 해야할까요? 다음 `exec_header.sh`파일을 jar 파일이 있는 폴더에 일단 복사합니다. `exec_header.sh`는 쉘스크립트이며 이 파일의 뒤에 동봉된 바이너리파일을 ‘실행’할 수 있도록 해줍니다.

```bash 
#!/bin/sh
#the file name is ‘exec_header.sh’
MYSELF=`which "$0" 2>/dev/null`
[ $? -gt 0 -a -f "$0" ] && MYSELF="./$0"
java=java
if test -n "$JAVA_HOME"; then
    java="$JAVA_HOME/bin/java"
fi
exec "$java" $java_args -jar $MYSELF "$@"
exit 1 
```

exec_header.sh에 jar파일을 다음 명령을 이용하여 동봉합니다. 

```bash 
cat exec_header.sh HelloWorld.jar > HelloWorld && chmod +x HelloWorld
```

자, 이제 HelloWorld를 실행할 준비가 모두 되었습니다. 다음 명령을 이용하여 실행해 봅시다.

```bash 
$ ./HelloWorld
```


### References

https://coderwall.com/p/ssuaxa

http://www.linuxjournal.com/content/add-binary-payload-your-shell-scripts


