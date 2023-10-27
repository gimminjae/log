# 배포과정 (ec2, rds, jenkins, docker, spring)
### 스왑메모리 할당 (ec2가 프리티어일 경우)
- https://github.com/gimminjae/log/blob/master/infra/docker/create-swapfile-in-linux.md
### docker 세팅
- https://github.com/gimminjae/log/blob/master/infra/docker/docker-setting.md
### jenkins 세팅
- https://github.com/gimminjae/log/blob/master/infra/docker/jenkins-setting.md
### Java version setting
```shell
# JDK 17 설치 방법 1 : jenkins_1 컨테이너에 접속해서 설치
docker exec -it jenkins bash
apt-get update
apt-get install openjdk-17-jdk -y

# mlocate 설치 및 검색
apt-get install mlocate
updatedb
locate java | fgrep 17 | fgrep javac
find : /usr/lib/jvm/java-17-openjdk-amd64

# JAVA_HOME 환경변수 변경 및 확인
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
echo $JAVA_HOME

# Jenkins 관리 > Global Tool Configuration
# Install automatically 체크 해제
# Name : openjdk-17-jdk
# JAVA_HOME : /usr/lib/jvm/java-17-openjdk-amd64
```
- [Blog](- https://github.com/gimminjae/log/blob/master/infra/docker/change-jenkins-java-version.md)
### Redis container setting
```
docker pull redis
docker run -d -p 6379:6379 --name redis-container redis
```
### 프로젝트 생성 및 세팅
- 
### docker.sock 설정
- 
### 
