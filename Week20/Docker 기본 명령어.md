# Docker 기본 명령어

### run - 컨테이너 실행

```bash
$ docker run [OPTIONS] IMAGE[:TAG|@DIGEST] [COMMAND] [ARG...]
```

|  Options  |                          설명                          |
| :-------: | :----------------------------------------------------: |
|    -d     |           백그라운드에서 실행(detached mode)           |
|    -p     |             호스트와 컨테이너 포트를 연결              |
|    -v     |      호스트와 컨테이너의 디렉토리를 연결(volume)       |
|    -e     |          컨테이너 내에서 사용할 환경변수 설정          |
|  --name   |                   컨테이너 이름 설정                   |
|   --rm    |           프로세스 종료시 컨테이너 자동 제거           |
|    -it    | -i와 -t를 동시에 사용한 것으로 터미널 입력을 위한 옵션 |
| --network |                     네트워크 연결                      |



run 명령어는 기본적으로 이미지가 존재하는지 확인하고 없다면 pull(다운로드)을 한 후 컨테이너를 생성한 후 실행하게 된다.



#### exec - 실행중인 도커 컨테이너 접속

ex) mysql 접속

```bash
$ docker exec -it mysql mysql
```



### ps - 컨테이너  목록 확인

```bash
$ docker ps [OPTION]
```

기본적으로 실행중인 컨테이너의 목록을 확인합니다.



| Option |              설명               |
| :----: | :-----------------------------: |
|   -a   | 중지되어 있는 컨테이너까지 확인 |



### stop - 실행중인 컨테이너 중단

```bash
$ docker stop [OPTIONS] CONTAINER [CONTAINER...]
```

실행중인 컨테이너를 중지하는 명령어

컨테이너를 하나 또는 여러개를 중지할 수 있다.



### rm - 종료된 컨테이너 삭제

```bash
$ docker rm [OPTIONS] CONTAINER [CONTAINER...]
```



### logs - 컨테이너의 로그 확인

```bash
$ docker logs [OPTIONS] CONTAINER
```

컨테이너가 출력하고있는 로그를 확인한다.

|    OPTIONS     |                        설명                        |
| :------------: | :------------------------------------------------: |
|       -f       | 로그를 출력하고 끝나는게 아닌 추적상태로 유지한다. |
| --tail [COUNT] | 마지막 줄 부터 COUNT의 수 만큼의 로그를 출력한다.  |



### images - 다운로드한 이미지의 목록을 출력한다

```bash
$ docker images [OPTIONS] [REPOSITORY[:TAG]]
```



### pull - 이미지를 다운로드한다.

```bash
$ docker pull [OPTIONS] NAME[:TAG|@DIGEST]
```



### rmi - 이미지를 삭제한다

```bash
$ docker rmi [OPTIONS] IMAGE [IMAGE...]
```



### network create - 가상 네트워크 생성

```bash
$ docker network create [OPTIONS] NETWORK
```

도커 컨테이너끼리 이름으로 통신할 수 있는 가상 네트워크를 만든다



### network connect - 가상 네트워크 연결

```bash
$ docker network connect NETWORK CONTAINER
```

