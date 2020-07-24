# 2020/02/07

## WebViewClient.onReceiveSslError() 의 보안상 이슈

[reference](http://theeye.pe.kr/archives/2721)

1. onReceiveSslError() : webview load 시 ssl 인증 에러 발생을 처리하는 callback 함수
2. 해당 콜백 함수에서 handler.proceed() 할 경우 ssl 오류를 발생시키지 않고 다음 동작을 실행함 => 보안 이슈
3. 해결법 : 해당 이슈 발생시 유저에게 에러가 발생했음을 알리고 그래도 실행할지를 물어보는 팝업을 띄움 

## APK Analyzer 
[reference](https://developer.android.com/studio/build/apk-analyzer?hl=ko)

어떤 곳에서 해당 함수를 호출했는지 (라이브러리 포함) 알고 싶을때 APK Analyzer의 dex 파일들을 확인해보면 가능

## Telegram 보안성?
[reference](http://road3.kr/?p=6383&cat=148)

### 보안성
1. 서버가 외국에 있고, 운영 규정상 정부 및 민간기관에 노출이 이루어지지 않음을 보장
2. 종단 간 이중 암호화 서비스 & MTP 프로토 클라우드를 이용한 오픈소스의 이중 암호화된 메시지 전달 가능
3. 자동 대화 내용 삭제 및 캡처 불가

### 취약점
1. 크랩터 보안 공격에 취약
2. 대화 메시지가 중앙 멀티 클라우드 내에 유지됨
3. 정부 기관에서 테러 및 범죄 방지 등을 위해 정보 제공 요청시 개발자와 운영진이 받아들일 경우 노출 가능
4. 복호화 프로그램이 존재

*** 완전한 보안 메신저는 아니다

## 구글 플레이 스토어 onReceiveSslError() 경고 메시지
상황 : 
1. 구글에서 WebViewClient.onReceiveSslError() 관련 경고 메일이 옴
2. 하지만 프로젝트 내에서 해당 콜백을 사용하지 않음
3. 그래서 다른 써드 파티 라이브러리에서 사용하고 있는지 확인 (APK Analyzer 이용)
4. 그래서 com.google.android.gms.internal.ads.zzbbv 에서 해당 콜백함수 사용하는 것을 확인
5. admob 관련 라이브러리 버전 업데이트 (com.google.firebase:firebase-ads: 18.2.0 -> 18.3.0 으로 업데이트)
6. 하지만 이게 실질적인 문제가 아니었음...
7. google play console > 출시 관리 > 사전 출시 보고서 > 보안 에서 해당 이슈를 확인할 수 있었음
8. com.bytedance.sdk.openadsdk.core.widget.webview.c 에서 해당 함수 호출했던 것을 확인
9. 결국 중국 광고 SDK (Pangolin)가 문제였던거임... 
