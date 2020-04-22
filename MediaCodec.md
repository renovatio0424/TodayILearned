# MediaCodec [(reference)](https://developer.android.com/reference/android/media/MediaCodec)
이 글은 안드로이드 미디어 코덱 문서를 번역 및 요약 정리한 글입니다. 

## MediaCodec 클래스란?

MediaCodec 클래는 low-level 미디어 코덱들에 접근하기 위해 사용되어 집니다. 즉, 인코더/디코더 컴포넌트입니다. 
이건 안드로이드 low-level multimedia support infrastructure 의 일부 입니다. 
(일반적으로 MediaExtractor, MediaSync, MediaMuxer, MediaCrypto, MediaDrm, Image, Surface, AudioTrack 와 함께 사용되어 집니다)
넓은 의미로 코덱은 인풋 데이터를 처리해 아웃풋 데이터를 생성합니다. 코덱은 비동기적으로 데이터를 처리하고 인풋 데이터와 아웃풋 데이터를 세트로 사용합니다. 
단순한 수준에서, 당신은 빈 인풋 버퍼를 요청하고, 그것을 데이터로 채우고, 코덱에서 데이터를 처리하도록 전달합니다. 
코덱은 그 데이터를 사용하고 그것을 빈 아웃풋 버퍼중 하나로 바꿔줍니다. 마침내 당신은 채워진 아웃풋 버퍼를 요청하거나 받고, 컨텐츠를 소비하고, 코덱으로 다시 릴리즈합니다.

## Data Types
코덱은 셋중 하나의 데이터를 가지고 작동합니다. 
1. compressed data
2. raw video data
3. raw audio data

이 세가지 데이터 모두 **ByteBuffer**를 사용해 처리 가능합니다. 하지만 raw video data로 코덱 성능을 향상시키려면 **Surface**를 사용해야만 합니다.
Surface 는 ByteBuffer에 mapping 또는 copying 없이 native video buffer 를 사용합니다. 그러므로 Surface가 훨씬 효율적입니다. 
Surface를 사용할때 당신은 일반적으로 raw video data에 접근할 수 없지만, 
**ImageReader** 클래스를 사용하여 암호화되지 않은 디코딩된 raw video 프레임에 접근할 수 있습니다. 
일부 기본 버퍼가 ByteBuffer # isDirect ByteBuffers에 매핑 될 수 있으므로 ByteBuffer를 사용하는 것보다 여전히 더 효율적일 수 있습니다.
ByteBuffer 모드를 사용할때, 당신은 **Image** 클래스와 **getInput/OutPutImage(int)** 를 사용하면서 raw video 프레임들에 접근할 수 있습니다. 

## Compressed Buffers
인풋 버퍼들(디코더를 위한) 와 아웃풋 버퍼들(인코더를 위한)은 **MediaFormat#KEY_MIME** 에 대한 compressed data 포함합니다. 
비디오 타입의 경우 일반적으로 하나의 압축 비디오 프레임 입니다. 
오디오 데이터의 경우 일반적으로 하나의 접근 단위 (format type 에 따라 일반적으로 수 밀리 초의 오디오를 포함하는 인코딩 된 오디오 세그먼트) 입니다 
그러나 버퍼에 여러 개의 인코딩 된 액세스 오디오 단위가 포함될 수 있다는 점에서이 요구 사항은 약간 완화됩니다.
두 경우 모두 버퍼는 임의의 바이트 경계에서 시작하거나 끝나지 않고 
BUFFER_FLAG_PARTIAL_FRAME으로 플래그가 지정되지 않는 한 프레임 / 액세스 단위 경계에서 시작 또는 끝납니다.

## Raw Audio Buffers
Raw Audio Buffer 는 PCM 오디오 데이터의 전체 프레임을 포함하며, 이는 채널 순서로 각 채널에 대해 하나의 샘플입니다.
각 PCM 오디오 샘플은 기본 바이트 순서로 모두 16 비트 signed integer 또는 float 입니다
float PCM 인코딩된 Raw audio buffer 는 오직 
Raw Audio Buffer 는 PCM 오디오 데이터의 전체 프레임을 포함하며, 이는 채널 순서로 각 채널에 대해 하나의 샘플입니다.샘
