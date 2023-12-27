---
title: Error response from daemon When using COPY with more than one source file
date: 2023-12-26 23:19
categories:
  - Docker
  - DockerError
tags:
  - DockerError
  - Docker
  - Gradle
image: 
path:
---

## 🌈 에러 발생 상황
스프링 프로젝트에서 build하기 위해 Dockerfile을 만든 후 다음과 같은 내용을 넣어주었다.

```shell
FROM amazoncorretto:17.0.9  

ARG JAR_FILE=target/*.jar  
COPY ${JAR_FILE} app.jar  

ENTRYPOINT ["java", "-jar", "/app.jar"]
```

이후 build를 하려 했는데, 다음과 같은 오류가 발생했다.
## 🌈 에러 로그 확인
```shell
Error response from daemon: When using COPY with more than one source file, the destination must be a directory and end with a /
Failed to deploy '<unknown> Dockerfile: Dockerfile': Can't retrieve image ID from build stream

```
![](/assets/img/IMG/Docker/Error/Error response from daemon When using COPY with more than one source file.png)


## 🌈 원인
한 개 이상의 파일을 COPY할 시, dst는 무조건 `/`로 끝나야 한다고 한다. 단순히 폴더를 지정해 줄 수도 있지만, 여기에는 조금 더 근본적인 원인이 있다.

![](/assets/img/IMG/Docker/Error/build.png)

COPY 명령어를 수행할 때 .jar 파일이 2개라서 해당 오류가 발생한 것이다! 그렇다면 이 plain.jar 파일은 무엇이며, 왜 생기는 것일까?
### 📌 Executable & Plain
빌드시 생성되는 jar 파일이 2개인 것을 확인할 수 있었는데, `파일명.jar(Executable)`과 `파일명-plain.jar(Plain)`이렇게 2개의 파일이 만들어진다. 이 두 파일의 차이점은 무엇일까?

먼저 Executable Jar는 java -jar 명령어로 실행시키면 구동이 되는데, 이는 당연히 jar에는 어플리케이션 구동에 필요한 **의존성들이 포함**되어 있기 때문이다.

하지만 Plain Jar는 Executable Jar와는 달리 **의존성을 포함하지 않고** 클래스와 리소스 파일만 포함되어 있다. 따라서 java -jar 명령어로 실행시킬 시 오류가 발생하게 된다.

### 📌 Plain Jar 생성 이유
SpringBoot 2.5 이상부터는 gradle 빌드 시 Jar 파일이 2개가 생성되도록 기본 설정이 되어 있기 때문이다.

## 🌈 해결
COPY 경로를 Executable Jar 파일로 확정지어도 되지만, 프로젝트에서는 Plain Jar 파일이 필요하다고 생각하지 않기 때문에 Plain Jar를 생성하지 않도록 했다.

build.gradle에 다음과 같은 코드를 추가하여 추가 생성을 막아준다.
```gradle
tasks.named("jar"){  
  enabled = false  
}
```