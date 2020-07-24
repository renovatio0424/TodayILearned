
## Media Container [(미디어 컨테이너 포맷)](https://developer.mozilla.org/ko/docs/Web/Media/Formats/%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88)

### 3GP
    - 셀룰러 네트워크를 통해 전송하고 모바일 장치에서 사용하기 위해 고안된 포맷
    - 원래 3G 모바일 폰을 위해 디자인하였지만 현대의 모바일 폰과 네트워크에서도 사용하고 있음
    - 하지만 네트워크 처리량이 늘어나면서 3GP 포맷의 필요성은 점차 줄어들고 있음
    - 하지만 여전히 느린 네트워크나 저사양 폰에서는 유용한 컨테이너임
    
  #### 셀룰러 네트워크 [(셀 (이동통신))](https://ko.wikipedia.org/wiki/%EC%85%80_(%EC%9D%B4%EB%8F%99_%ED%86%B5%EC%8B%A0))
    - 이동 통시에서는 하나의 주파수 대역에 다수의 사용자를 수용하기 위해 다중 접속 기술을 사용함
    - 하지만 일정 이상의 사용자가 접속하면 채널 포화가 일어나 서비스 이용이 어려움
    - 그래서 제한된 주파수 자원을 효율적으로 사용하기 위해 넓은 지역을 나누고 셀 중간에 위치한 기지국이 특정 주파수를 사용하여 서비스를 제공
    - 인접하지 않은 기지국 끼리는 다시 동일한 주파수를 재활용함으로써 주파수 이용 효율을 높임 
    
### ADTS (Audio Data Tansport Stream)
    - 인터넷 라디오 같은 오디오 스트림을 사용하기 위해 MPEG-4 Part3로 규정된 컨테이너 포맷
    - 근본적으로 ACC 오디오 데이터에서 스트림만 깐 것과 거의 동일
    - 최소한의 헤더만 담긴 ADTS 프레임으로 구성
    
### FLAC (Free Lossless Audio Codec) 
    - 무손실 오디오 코덱
    - 어느 특허에 묶여 있지 않아 자유롭게 사용가능
    - FLAC 오디오 데이터만 담을 수 있음
    
### MPEG/MPEG-2
    - MPEG-1 과 MPEG-2는 근본적으로 동일
    - the Moving Picture Experts Group (MPEG) 에서 만듬
    - DVD 등 물리적 매체에서 널리 사용됨
    - MP3(MPEG-1 Audio Layer 3) 파일로 널리 사용됨
    
### MPEG-4 (MP4)
    - 최신 MPEG 파일 포맷
    - 미디어 타입을 표기할때 codec 파라미터를 추가하여 오디오/비디오 코덱을 명시할 수 있음
    
### WebM (Web Media)
    - Matroska 에서 현대 웹 환경에서 사용하기 위해 디자인됨
    - 기본적으로 무료 오픈 코덱을 사용하여 완전한 자유-오픈 기술 지향
    
### OGG
    - Xiph.org Foundation 이 운영하는 자유 오픈 컨테이너 포맷
    - Ogg 프레임워크 (Theora, Vorbis, Opus)는 특허에 얽메이지 않게 정의됨
    
### WAVE (WAV)
    - Waveform Audio File Format (WAVE) 는 보통 중려서 WAV라 불리고 .wav 확장자를 가짐
    - 오디오 비트스트림 데이터를 담기 위해 Microsoft & IBM 이 개발
    - Linear PCM 포맷의 오디오 데이터를 담고 있음
    - Resource Interchange File Format (RIFF) 에서 파생됨


