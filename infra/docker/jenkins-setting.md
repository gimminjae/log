# image pull
```
docker pull jenkins/jenkins:lts
docker pull jenkins/jenkins:jdk17
```
# confirm image
```
docker images
```
# run image
```
docker run -d -p 9080:8080 -v /var/run/docker.sock:/var/run/docker.sock -v /var/jenkins_home:/var/jenkins_home --name jenkins -u root jenkins/jenkins:lts # :jdk17
```
### Option
- "-d" : background 실행
- "-v" : 도커 내부와 외부를 연결
- "--name" : 생성되는 컨테이너의 이름, 생략시 무작위 생성
- "-u" : user 지정 -> 추후에 권한 문제 방지를 위해 root 권한으로 실행

# confirm running container
```
docker ps
```
- "-a" : 옵션 추가시 모든 컨테이너 확인

# print running container's logs
```
docker logs [container name]
docker logs jenkins
```
# enter container console
```
docker exec -it [container name]
docker exec -it jenkins
```
- "-u root" : root 권한으로 실행
# get password
```
cat /var/jenkins_home/secrets/initialAdminPassword
```

# Jenkins 세팅
- install plugin
- enter account info
- ...

  
