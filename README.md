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

# 2025-08-10
## 라즈베리파이 Telegram API 설치
### 파이썬 깔기
```
sudo apt install python3-pip

```
#### error: externally-managed-environment
- rm : 지우기
```
sudo rm /usr/lib/python3.@@(버전)/EXTERNALLY-MANAGED
```
### Telegram API 설치
```
pip3 install python-telegram-bot --upgrade
```

## 라즈베리파이 + Telegram 연동하기
- 라즈베리파이 Telegram API 사이트 : https://pypi.org/project/python-telegram-bot/
### git 깔기
```
sudo apt install git
```
### 라즈베리파이 Telegram API 사용
```
git clone https://github.com/python-telegram-bot/python-telegram-bot --recursive
```
## 라즈베리파이 카메라 이용
### 파이썬 파일 들어가기
- ls : 파일 보기
- cd : 파일 열기
```
cd python-telegram-bot/examples/
```
```
sudo vim timerbot.py
```
- vim 없을 때
```
sudo apt install vim
```


### TimerBot 수정
- 파이썬 창에서 "(TOKEN)"에 내 Telegram 토큰 넣기
- 끝
## 라즈베리파이 Telegram로 할 수 있는 것
### 작동 방법
- Telegram앱에 봇 채팅에서 '/'치고 함수입력으로 봇과 채팅 가능 (예 : /start, /set)
```
python3 timerbot.py
```
- Ctrl + c 로 중단
### 수정
- 파이썬 창에서 수정 가능(예시)
```
def main() -> None:
    """Run bot."""
    # Create the Application and pass it your bot's token.
    application = Application.builder().token("8484920007:AAGzu0AmrqOSj5tfb404k2pKQRmcG-dBlX4").build()

    # on different commands - answer in Telegram
    application.add_handler(CommandHandler(["start", "help"], start))
    application.add_handler(CommandHandler("ty",s))
    application.add_handler(CommandHandler("set", set_timer))
    application.add_handler(CommandHandler("unset", unset))

    # Run the bot until the user presses Ctrl-C
    application.run_polling(allowed_updates=Update.ALL_TYPES)
```
- application.add_handler(CommandHandler(["start", "help"], start)) 부분에서 "start" 부분이 함수 호출 부분

```
async def start(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Sends explanation on how to use the bot."""
    await update.message.reply_text("Hi! Use /set <seconds> to set a timer")

async def s(update: Update, context: ContextTypes.DEFAULT_TYPE) -> None:
    """Sends explanation on how to use the bot."""
    await update.message.reply_text("서호진 멍청이")


async def alarm(context: ContextTypes.DEFAULT_TYPE) -> None:
    """Send the alarm message."""
    job = context.job
    await context.bot.send_message(job.chat_id, text=f"Beep! {job.data} seconds are over!")
```
- 함수 추가 및 원하는 기능 추가 가능(예 : 집 불 끄기, 온도 확인, 전력 확인, 등등)
