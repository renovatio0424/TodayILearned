# 2020/04/29

## H.264 (Video Codec)[(위키)](https://ko.wikipedia.org/wiki/H.264/MPEG-4_AVC)

### H.264 란?
    - 블록 단위 움직임 보상 기반의 영상 압축 표준
    - H.264, MPEG-4 파트 10, Advanced Video Coding (MPEG-4 AVC)라고 불림
    - 동영상 녹화, 압축, 배포를 위한 방식들 중 현재 가장 보편적으로 사용되고 있는 포맷
    
### 목적
    1. 압출율이 좋고
    2. 실용적이고
    3. 개발하기 쉽고
    4. 좋은 품질의 비디오를 제공
    
### YUV [(YUV에 대해)](https://m.blog.naver.com/PostView.nhn?blogId=wndrlf2003&logNo=220253497246&proxyReferer=https:%2F%2Fwww.google.com%2F)
: 색을 표현하는 포맷

#### RGB vs YUV
- RGB : 색 그대로 (빨강, 파랑, 초록의 비율)로 나타냄
- YUV : 밝기(Y)와 색상 신호 2개(U,V)로 나타냄
    
#### 서브 샘플링
YUV 숫자3개 : 각 요소들의 비율을 나타냄

ex: YUV 422 -> Y : U : V = 4 : 2 : 2

- YUV 444 
- YUV 422
- YUV 420 
- YUV 411
