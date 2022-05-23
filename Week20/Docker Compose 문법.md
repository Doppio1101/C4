# Docker Compose 문법

### version

```yaml
version : '3'
```

docker-compose.yml 파일의 명세 버전

버전에 따라 지원하는 도커 엔진 버전이 다르다.

### 

### service

```yaml
services:
	backend:
		...
		
	frontend:
		...
```

실행할 컨테이너 정의

docker run --name backend와 같다고 생각할 수 있다.



### image

```yaml
services:
	backend:
		image: skdltm117/backend:0.1
```

컨테이너에 사용할 이미지 이름과 태그

태그를 생략하면 latest 이미지로 실행되며

이미지가 없으면 자동으로 pull을 받는다.



### ports

```yaml
services:
	backend:
		...
		ports:
		 -"8080:8080"
```

컨테이너와 연결할 포트 {호스트포트}:{컨테이너 포트}



### environment

```yaml
services:
	mysql:
		...
		environment:
			MYSQL_ROOT_PASSWORD:"root"
```

컨테이너에서 사용할 환경변수 {환경변수 이름}:{값}



### volumes

```yaml
services:
	backend:
		...
		volumes:
		 - ./app:/dir
```

마운트하려는 디렉터리 {호스트 디렉터리}:{컨테이너 디렉터리}



### restart

```yaml
services:
	backend:
		restart: always
```

재시작 정책

no : 수동으로 재시작

always : 수동으로 끄기 전까지 항상 재시작

on-failuer: 오류가 있을 시 재시작

unless-stopped: 명시적으로 중지되거나, Docker 자체가 중지되는 경우 재시작



### build

```yaml
service:
	backend:
		build:
			context: {dockerfile 경로}
			dockerfile: {dockerfile명}
```

이미지 자체를 빌드 후 사용

image 속성 대신 사용한다.

여기에 사용할 별도의 도커파일 필요.