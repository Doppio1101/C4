# Docker Image 만들기

### 기존의 이미지를 가져와 다른 이미지 만들기

```bash
$ docker commit CONTAINER IMAGE_NAME
```



ex) ubuntu 이미지를 가져와 git이 설치된 ubuntu를 다시 이미지로 만들기

```bash
$ docker run -it name git ubuntu bash

# apt-get update
# apt-get install -y git

# 컨테이너를 종료하지 않고 새 터미널로
$ docker commit git ubuntu:git
```

위 과정을 진행하면 태그명이 git인 새 ubuntu이미지가 생성된다.



### DockerFile을 이용해 이미지 빌드하기

```bash
$ docker build -t DockerHubId/IMAGE_NAME[:TAG]
```



### DockerFile

| 예약어     | 설명                                                 |
| ---------- | ---------------------------------------------------- |
| FROM       | 기본이 될 이미지                                     |
| RUN        | 쉘 명령어 실행                                       |
| CMD        | 컨테이너 기본 실행 명령어 (Entrypoint의 인자로 사용) |
| EXPOSE     | 오픈되는 포트 정보                                   |
| ENV        | 환경변수 설정                                        |
| ADD        | 파일 또는 디렉토리 추가. URL/ZIP 사용 가능           |
| COPY       | 파일 또는 디렉토리 복사                              |
| ENTRYPOINT | 컨테이너 기본 실행 명령어                            |
| VOLUME     | 외부 마운트 포인트 생성                              |
| USER       | RUN, SMD, ENTRYPOINT를 실행하는 사용자               |
| WORKDIR    | 작업 디렉토리 설정                                   |
| ARGS       | 빌드타임 환경변수 설정                               |
| LABEL      | key - value 데이터                                   |
| ONBUILD    | 다른 빌드의 베이스로 사용될 때 사용하는 명령어       |



