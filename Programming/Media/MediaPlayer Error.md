# 2020/05/04

## MediaPlayer Error (failure code:-32)

### 에러코드 

MediaPlayer 구현했을때 다음과 같은 에러를 종종 본다

~~~java
Fatal Exception: java.lang.RuntimeException
failure code: -32
    android.media.MediaPlayer.invoke (MediaPlayer.java:693)
    android.media.MediaPlayer.getInbandTrackInfo (MediaPlayer.java:1926)
    android.media.MediaPlayer.scanInternalSubtitleTracks (MediaPlayer.java:2083)
    android.media.MediaPlayer.access$600 (MediaPlayer.java:552)
    android.media.MediaPlayer$EventHandler.handleMessage (MediaPlayer.java:2565)
    android.os.Handler.dispatchMessage (Handler.java:102)
~~~

### 해결 방법
1. MediaPlayer 에 MediaPlayer.setOnErrorListener 를 달기
2. 에러 코드를 추적하기
3. 에러코드에 대한 상세 내용은 이 [링크](https://developer.android.com/reference/android/media/MediaPlayer#constants_1)를 참고

** 에러를 해결하기 네이티브 코드를 확인하는 일이 없길 바란다 ...

