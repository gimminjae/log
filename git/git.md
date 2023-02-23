## 초기 설정
```
이름, 이메일 설정
git config --global user.name "your_name"
git config --global user.email "your_email"

설정 정보 보기
git config --list
```
## 프로젝트 git에 올리기
- 처음 올릴 때
```
초기화
git init

깃헙 레포 연결
git remote add origin https://github.com/bitnaGithub/firstproject.git

연결 확인
git remote -v
```
- 코드 올리기
```
git add .
git commit -m "commit message"
git push origin master
```

- 현재 상태 확인
```
git status
```

## 깃헙에서 프로젝트 받기
- 깃헙 레포에서 Download Zip
- 클론
```
git clone 깃헙레포주소url
```
- remote 후 pull
```
git remote add origin 깃헙주소
git pull (origin master)
```
- 협업 시 다른 사람의 작업 내용 받기
```
git pull
git pull origin master(브랜치 이름)
```
## 브랜치
- 브랜치 생성 및 이동
```
git branch 브랜치이름
git checkout 브랜치이름
```
- 위의 두 명령어 축약(브랜치 생성과 동시에 이동)
```
git checkout -b 브랜치이름
```
## 커밋 히스토리 보기
- 기본
```
git log
```
- 옵션 넣어 보기
```
git log --oneline --graph
```
## local remote 와 동일하게 업데이트(동기화)
```
git remote update
```
