# PostgreSQL 설치 및 세팅 방법

1. 아래 사이트 접속하여 Docker 설치 진행  
[Docker](https://www.docker.com/get-started/)

2. Docker 구동 중 WSL Update 필요하다는 메세지 발생 시 하기 링크에서 다운로드 받기  
[Linux 커널 업데이트 패키지 다운로드](https://docs.microsoft.com/ko-kr/windows/wsl/install-manual#step-4---download-the-linux-kernel-update-package)

### 1. PostgreSQL 컨테이너와 연결 할 볼륨을 설정
```bash
docker volume create pgdata[볼륨명]
```
- 볼륨을 지정해 주면 컨테이너가 삭제되어도 정보는 유지되기 때문에 DB 사용 시 필수적으로 고려해야 할 사항이다.

### 2. PostgreSQL 컨테이너 설정
```bash
docker run -p 5432:5432 --name postgres -e POSTGRES_PASSWORD=root -d -v pgdata:/var/lib/postgresql/data postgres
```
- docker run -p [외부포트]:[컨테이너포트] --name [컨테이너 이름] -e POSTGRES_PASSWORD=[비밀번호] -d -v [볼륨정보] [이미지]

### 3. 컨테이너 Bash 접속
- CMD 접속
    ```bash
    docker exec -it postgres /bin/bash
    ```
- Docker 앱에서 버튼으로 들어갈 수 있다.

### 4. DB 생성
- postgres로 접속한다.
    ```bash
    psql -U postgres
    ```

- 사용자를 생성한다.
    ```sql
    CREATE role usernm WITH password 'mypassword';
    ```

- TABLESPACE를 생성한다.
    ```sql
    CREATE TABLESPACE TS_NAME owner usernm LOCATION '/var/lib/postgres/data';
    ```

- DB를 생성한다.
    ```sql
    CREATE DATABASE DBNAME WITH owner=usernm TABLESPACE=TS_NAME;
    ```

### 5. 생성한 유저로 DB 연결