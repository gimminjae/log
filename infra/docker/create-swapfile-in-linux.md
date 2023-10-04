# create swap-memory
### 상태 확인
```
free -h
```
### dd 명령을 사용하여 루트 파일 시스템에 스왑 파일 생성
bs : 블록 크기, count : 블록의 수

지정한 블록 크기는 인스턴스에서 사용 가능한 메모리보다 작아야 한다. (그렇지 않을 시, memory exhausted 오류가 발생한다.)

권장사항에 의하면 스왑 공간 크기는 RAM 용량의 2배를 권장했으므로
2GB 증설시켜야 한다. (128MB x 16 = 2.048MB)
```
sudo dd if=/dev/zero of=/swapfile bs=128M count=16
```
### 스왑 파일에 대한 읽기 및 쓰기 권한을 업데이트
```
sudo chmod 600 /swapfile
```
### Linux 스왑 영역 설정
```
sudo mkswap /swapfile
```
### 스왑 공간에 스왑 파일을 추가
스왑 파일을 즉시 사용할 수 있도록 만든다
```
sudo swapon /swapfile
```
### 절차가 성공했는지 확인
```
sudo swapon -s
```
### /etc/fstab 파일을 편집
부팅 시 스왑 파일을 활성화
```
sudo vi /etc/fstab
# add this
# /swapfile swap swap defaults 0 0
```
### 스왑메모리 확인
```
free -h
```
