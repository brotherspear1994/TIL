# Docker를 이용한 배포 기초

- AWS에 도커 설치 후 도커에 mySql 설치

  ## AWS에 도커 설치

  ```
  HTTPS를 통해 repository를 사용할 수 있도록 패키지 설치
  ```

  - sudo apt update : 설치는 apt를 이용해서 설치할 것임.

- sudo apt install apt-transport-https

  - sudo apt install ca-certificates

- sudo apt install curl : 컬은 특정한 웹사이트에서 데이터를 다운받을때 사용.

  - sudo apt install software-properties-common

  ### Docker 공식 GPG 키 등록

  - curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -

  ### 저장소 설정

  - sudo add-apt-repository “deb [arch=amd64] https://download.docker.com/linux/ubuntu bionic stable”
  - sudo apt update

### 도커설치

- apt-cache policy docker-ce

  - sudo apt install docker-ce

  ### 도커는 설치하면 자동으로 시스템 서비스로 등록돼서 언제 어디서나 편하게 부를 수 있음.

  - sudo systemctl status docker

  ### TEST로 hello-world 띄어줌.

- sudo docker pull hello-world

  - 실제로 컨테이너로 만들어 띄어보는 것. 곧바로 우리 서버위에 하나의 서버가 별도로 생성됨.
  - sudo docker run hello-world

  ### 어떤 컨테이너가 동작했는지 확인

  - sudo docker ps -a (모든 컨테이너 조회)(현재 실행중인 것만 조회 하려면 -a 생략)

    (CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES)

  ### 해당 도커 컨테이너 삭제

  - sudo docker rm {CONTAINER ID}

  ### 컨테이너 중지

  sudo docker stop {CONTAINER ID}

  ### 이미지 파일 확인

  - sudo docker images(REPOSITORY TAG IMAGE ID CREATED SIZE)

## 도커에 MySQL 설치

MySQL의 경우는 docker에 기본적으로 탑재되어 있는 이미지이므로 설치없이 다운받아 바로 실행 가능

##### mysql 실행

- docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=ssafy -d mysql:8.0

  (도커허브에서 mysql 8.0버전 다운받기)

  ### 컨테이너의 데이터를 호스트 OS에 저장하기

- 컨테이너를 제거하면 데이터도 함께 제거된다.

- 그래서 컨테이너의 데이터를 호스트 OS에 저장하기

  - 도커는 컨테이너를 docker run 명령어로 생성할 때 컨테이너의 특정 디렉터리와 호스트 OS의 특정 디렉터리를 서로 공유할 수 있도록 -v [호스트의 디렉터리]:[컨테이너의 디렉터리] (또는 –volume)옵션을 제공

- aws 우분투에 폴더만들고, 기존 컨테이너를 종료 후 -v 옵션을 추가해 마운트 시킨다.( 컨테이너와 호스트가 디렉터리를 공유한다 라는 말이 맞을 수 있지만 그보다는 호스트의 특정 디렉터리(지정해준)를 컨테이너의 특정 경로에 마운트 시킨다 라고 할 수 있다.)

  - sudo docker run -d -p 3306:3306 -e MYSQL_ROOT_PASSWORD=ssafy -d -v /home/ubuntu/mysql:/var/lib/mysql –name boraCoin-mysql mysql:8.0

(도커허브에서 mysql 8.0버전 다운받고) (mysql 호스트 os 디렉토리 연결) 이 과정을 해주지 않으면 컨테이너 데이터가 항상 초기화 됨

docker ps -a 로 컨테이너 실행정보 조회하기

(CONTAINER ID IMAGE COMMAND CREATED STATUS PORTS NAMES bf33cf422c0d mysql:8.0 “docker-entrypoint.s…” 29 minutes ago Up 29 minutes 0.0.0.0:3306->3306/tcp, 33060/tcp bold_lederberg) 이렇게 나오면 성공

- docker exec -it 2186c22774d2(mysql 컨테이너 ID) /bin/bash (도커 mysql 컨테이너 실행, bash 형태)
- mysql -u root -p (password : ssafy)
- docker inspect bf33cf422c0d(container ID) (도커 컨테이너 세부정보 확인)
- sudo apt install mysql-client-core-5.7 (AWS ubuntu 인스턴스에 mysql 설치)
- mysql -u root -p –host 172.26.2.234(ip address) –port 3306(AWS에서 바로 mysql 접속하기)

### 테이블 생성 및 사용자 권한 부여

### 사용자생성 및 권한 부여

사용자 아이디와 비번 = certi/ssafy

### 유저생성

- CREATE USER ‘certi’@‘%’ IDENTIFIED BY ‘ssafy’;(MySQL certi, 암호 ssafy로 설정, 외부에서 접속가능하기 위해 %)

### 유저권한부여

- grant all privileges on *.* to ‘certi’@‘%’; (권한주기)
- show grants for ‘certi’@‘%’;(권한보기)

### 스키마 생성

- create database certi;

------

위에 과정 까지 진행 완료 했습니다. 배포시 아래를 진행해야합니다.

------

# 백엔드, 프론트엔드 배포

## 백엔드 배포

- 자바 JAR File 이란?

  - 일종의 자바 프로젝트 압축 파일
  - JAR 파일은 웹브라우저에서 빠르게 다운로드할 수 있도록, 자바 애플릿을 위한 클래스, 이미지 및 사운드 파일들을 하나의 파일에 압축하여 담고 있는 파일
  - https://galid1.tistory.com/428 블로그를 참고하여 jar파일을 만듦

- AWS에서

  - docker pull rtfpessoa/ubuntu-jdk8
  - vi ./Dockerfile
  - 입력
    - FROM rtfpessoa/ubuntu-jdk8 ADD haribo-1.0.0.jar certi.jar ENV JAVA_OPTS="" ENTRYPOINT [“java”,“-jar”,“/certi.jar”]
  - docker build –tag certi:0.1 ./

- docker run -d -p 8080:8080 certi:0.1 ## 프론트엔드 배포

- Nginx로 실행

  - 트래픽이 많은 웹사이트를 위해 확장성을 위해 설계한 비동기 이벤트 기반구조의 웹서버 소프트웨어

- Nginx Docker 설치하기

  - 참고블로그 : 

    https://minimilab.tistory.com/8

    - sudo docker pull nginx:latest
    - AWS에 폴더만들어서 프론트엔드 옮겨놓음
    - docker run –name nginx-certi -v /home/ubuntu/{파일경로}:/usr/share/nginx/html:ro -d -p 80:433 nginx

# 백엔드, 프론트엔드 재배포

## 백엔드 재배포

- docker ps에서 확인해서 전에 올렸던 jar 컨테이너를 중지 or 삭제한다.
- jar 파일 다시 올려서 aws 폴더에 올린다.
- docker build –tag certi:0.2 ./
- docker run -d -p 8080:8080 certi:0.2
- 컨테이너에 도커 이미지 폴더 추가 – 이미지 파일 추가시 개념
  - 도커 컨테이너
    - 도커 컨테이너 접속
      - docker exec {container id} ls /
  - docker cp /home/ubuntu/certi/worksImage {container id}:/
    - 참고 : https://www.reddit.com/r/docker/comments/6xvk7o/how_do_we_copy_a_folder_from_host_to_container/
- 주의할 점 : 도커 컨테이너 안에 도커 이미지 폴더에 이미지가 추가되므로 DB에는 연동되지만, 우리 개발 환경의 도커 이미지 폴더에는 연동되지않음!

## 프론트엔드 재배포

- 프론트엔드는 컨테이너 중지시킨 후, 프론트엔드 폴더만 AWS에 바꿔주고 다시 재시작
  - docker stop ‘이미지ID’
  - docker restart ‘이미지ID’

---

참고 레퍼런스 : https://galid1.tistory.com/320?category=763527