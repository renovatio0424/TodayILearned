
## 와이파이로 ADB 연결하기 

### 1. CLI 로 연결하기 ([미르의 IT 정복기])(https://itmir.tistory.com/594)


    1. 먼저 컴퓨터와 스마트폰이 같은 Wifi 또는 공유기에 연결해주세요
    2. 먼저 스마트폰을 컴퓨터에 USB로 연결해주세요
    3. cmd창을 하나 열으신다음 아래 명령어를 입력해주세요
       
       adb tcpip 5555
       
       * 물론 adb가 들어있는 폴더에서 cmd를 작업해주시거나 환경변수를 설정하셔야 합니다.
         5555는 연결할 포트입니다.
       
       * 성공시 나타나는 내용 : restarting in TCP mode port: 5555

    4. 이제 USB를 연결해제하세요
       그다음 스마트폰의 IP주소를 알아내야 합니다.

        1) 설정 앱 - 휴대폰 정보 - 상태(또는 네트워크) - IP 주소
        2) 설정 앱 - WIFI - WIFI 고급 설정(또는 WIFI 설정) - IP 주소

    5. 찾은 IP로 연결합니다. 
       
       adb connect <Your IP>:5555

       * 성공시 나타나는 내용 : connected to <IP>:5555
      

### 2. plugin 으로 연결하기 ([Devgoogry](https://googry.tistory.com/23))
    
    1. Preference(Command + ,) -> Plugins -> Browse Repositories... -> wifi adb ultimate 검색
    2. install & restart android studio
    3. connect usb cable with your device
    4. click Play button 
    
![wifi adb ultimate](https://t1.daumcdn.net/cfile/tistory/99361C3359993DAC0C)