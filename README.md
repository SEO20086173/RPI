# RPI
## 라즈베리파이 한국어 설정
  - 터미널 오픈 후 한글 입력기로 ibus 설치
```
sudo apt update
sudo apt upgrade
```
```
sudo apt-get install fonts-unfonts-core -y
sudo apt-get install ibus ibus-hangul -y
sudo reboot
```
  - 입력기로 ibus 지정
    - 기본 설정 -> 입력기 -> "예(Y)"선택 -> "ibus"선택 후 확인
  - ibus 기본 설정
    - 기본 설정 -> iBus 기본 설정 -> "추가"선택 -> "한국어 - Hangul"선택
  - 키보드 레이아웃 설정
    - 기본 설정 -> 키보드와 마우스 -> 키보드 탭 -> 레이아웃에서 한국어 선택 -> 확인

## InfluxDB 설치
  - 터미널로 InfluxDB 다운로드
```wget -q https://repos.influxdata.com/influxdata-archive_compat.key
echo '393e8779c89ac8d958f81f942f9ad7fb82a25e133faddaf92e15b16e6ac9ce4c influxdata-archive_compat.key' | sha256sum -c && cat influxdata-archive_compat.key | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/influxdata-archive_compat.gpg > /dev/null
echo 'deb [signed-by=/etc/apt/trusted.gpg.d/influxdata-archive_compat.gpg] https://repos.influxdata.com/debian stable main' | sudo tee /etc/apt/sources.list.d/influxdata.list
```
  - 최신 상태인 InfluxDB 설치
```
 sudo apt-get update && sudo apt-get install influxdb -y
```
  - 시작 시 백그라운드 서비스로 InfluxDB 사용
```
sudo service influxdb start
```
  - InfluxDB 상태 확인(?)
```
sudo service influxdb status
```

##다음다음다음
# ------------------
# 2025-08-10
## 라즈베리파이 Telegram API 설치
```
pip3 install python-telegram-bot --upgrade
```
### 파이썬 깔기
```
sudo apt install python3-pip

```
#### error: externally-managed-environment
- rm : 지우기
```
sudo rm /usr/lib/python3.@@(버전)/EXTERNALLY-MANAGED
```
