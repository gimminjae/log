# install java ex)17 version
```
apt-get update
apt-get install openjdk-17-jdk -y
```

# mlocate 설치 및 검색
```
apt-get install mlocate
updatedb
locate java | fgrep 17 | fgrep javac
# find : /usr/lib/jvm/java-17-openjdk-amd64
```
# change JAVA_HOME
```
export JAVA_HOME=/usr/lib/jvm/java-17-openjdk-amd64
```

# confirm JAVA_HOME
```
echo $JAVA_HOME
# -> /usr/lib/jvm/java-17-openjdk-amd64
```

# confirm java version
```
java -version
```
# 추가 작업 - jenkins
시스템 환경 변수 JAVA_HOME이 17을 가르치게 했지만 젠킨스는 자체적으로 JAVA_HOME이 11을 가르키고 있다. 

따라서 추가 작업이 필요하다.

- Jenkins 관리
- Global Tool Configuration
- Install automatically 체크 해제
- Name : openjdk-17-jdk
- JAVA_HOME : /usr/lib/jvm/java-17-openjdk-amd64
