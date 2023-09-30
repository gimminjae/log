# image pull
```
docker pull jenkins/jenkins:lts
```
# confirm image
```
docker images
```
# run image
```
docker run -d -p 9080:8080 -v /var/run/docker.sock:/var/run/docker.sock --name jenkins jenkins/jenkins:lts
```
### Option
- "-d" : background 실행
- "-v" : 도커 내부와 외부를 연결
- "--name" : 생성되는 컨테이너의 이름, 생략시 무작위 생성

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
# get password
```
cat /var/jenkins_home/secrets/initialAdminPassword
```

