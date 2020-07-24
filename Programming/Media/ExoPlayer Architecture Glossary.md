# 2020/04/28

## 1. ExoPlayer Architecture Glossary

![exoplayer architecture](https://exoplayer.dev/images/glossary-exoplayer-architecture.png)

1. BandwidthMeter
    - 데이터 전송을 감지하면서 네트워크 대역폭을 측정하는 컴포넌트
    - Adaptive streaming 에서 대역폭 측정은 재생하는 동안 서로 다른 비트레이트들 중에 선택가능하도록 해줍니다. 
    
2. DataSource
    - 데이터(HTTP를 통해, 로컬 파일들로 부터 등등)를 요청하는 컴포넌트

3. Extractor
    - 미디어 컨테이너 포맷을 파싱하여 트랙 정보출력
    - 디코더에 맞는 각각의 트랙에 속해있는 개별 접근 단위들로 출력하는 컴포넌트 

4. LoadControl
    - 재생을 시작할때와 로딩의 시작과 멈춰야하는 때를 결정하는 컴포넌트

5. MediaSource
    - 타임라인처럼 미디어의 구조들에 대한 고수준 정보들 제공
    - 타임라인 주기들에 상응하는 MediaPeriod 인스턴스 생성
    
6. MediaPeriod
    - 하나의 미디어 조각(오디오 파일, 광고, 두 광고 사이에 인터리브된 콘텐츠 등등)을 로드
    - 로드된 미디어를 읽을 수 있도록 (전형적으로 Renderer에 의해) 허용함
    - 해당 미디어 안에 어떤 트랙들을 로드될 것인지, 언제 로딩을 시작하고 멈출지에 대한 결정들은 TrackSelector 와 LoadControl이 각각 합니다. 
    
7. Renderer
    - 미디어 샘플들을 읽고, 디코딩하고 렌더링하는 컴포넌트입니다. 
    - Surface 와 AudioTrack들은 비디오와 오디오 데이터를 렌더링하는 안드로이드 플랫폼의 기준 컴포넌트입니다. 
    
8. Timeline 
    - 단순한 구조 (하나의 미디어만 있는 경우) 부터 재생목록이나 광고가 삽입된 재생목록 및 스트림과 같은 복잡한 미디어 구성을 표현합니다. 
    
9. TrackGroup
    - 일반적으로 적응형 스트리밍을 위해 서로 다른 비트 전송률로 동일한 비디오, 오디오 또는 텍스트 컨텐츠의 하나 이상의 표현을 포함하는 그룹입니다.

10. TrackSelection 
    - TrackGroup에서 트랙의 정적 서브 세트와 서브 세트에서 선택 가능한 다양한 트랙으로 구성된 Selection
    - 적응형 스트리밍의 경우 TrackSelection은 새 미디어 청크가 로드되기 시작할 때마다 적절한 트랙을 선택합니다.
    
11. TrackSelector
    - 재생할 트랙을 선택합니다
    - 플레이어의 렌더러의 기능과 함께 재생할 MediaPeriod에 대한 트랙 정보가 제공되면 TrackSelector는 각 렌더러에 대한 TrackSelection을 생성합니다.
    


