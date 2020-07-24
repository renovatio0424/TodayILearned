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
Raw Audio Buffer 는 PCM 오디오 데이터의 전체 프레임을 포함하며, 이는 채널 순서로 각 채널에 대해 하나의 샘플입니다. 

float PCM 인코딩된 Raw Audio Buffer는 **MediaCodec # configure (…)** 로 MediaFormat의 **MediaFormat # KEY_PCM_ENCODING**이 **AudioFormat # ENCODING_PCM_FLOAT**로 설정되고 디코더의 경우 **getOutputFormat()** 또는 인코더의 경우 **getInputFormat()** 으로 확인 된 경우에만 가능합니다.

~~~java
static boolean isPcmFloat(MediaFormat format) {
  return format.getInteger(MediaFormat.KEY_PCM_ENCODING, AudioFormat.ENCODING_PCM_16BIT)
      == AudioFormat.ENCODING_PCM_FLOAT;
}
~~~

짧은 배열로 16bit signed 된 integer audio data를 추출하기 위해 아래 코드를 사용하면 됩니다.

~~~java
 // Assumes the buffer PCM encoding is 16 bit.
short[] getSamplesForChannel(MediaCodec codec, int bufferId, int channelIx) {
  ByteBuffer outputBuffer = codec.getOutputBuffer(bufferId);
  MediaFormat format = codec.getOutputFormat(bufferId);
  ShortBuffer samples = outputBuffer.order(ByteOrder.nativeOrder()).asShortBuffer();
  int numChannels = format.getInteger(MediaFormat.KEY_CHANNEL_COUNT);
  if (channelIx < 0 || channelIx >= numChannels) {
    return null;
  }
  short[] res = new short[samples.remaining() / numChannels];
  for (int i = 0; i < res.length; ++i) {
    res[i] = samples.get(i * numChannels + channelIx);
  }
  return res;
 }
~~~

## Raw Video Buffers
ByteBuffer 모드에서 비디오 버퍼들은 **MediaFormat#KEY_COLOR_FORMAT** 에 따라 배치되게 됩니다. 
당신은 다음의 API로부터 지원되는 color format들을 배열로서 받을 수 있습니다

1. getCodecInfo()
2. MediaCodecInfo#getCapabilitiesForType
3. CodecCapabilities#colorFormats

비디오 코덱들은 3가지 종류의 color format들을 지원합니다. 

1. native raw video format 

    CodecCapabilites#COLOR_FormatSurface로 표시되며, input / output Surface 와 사용 가능합니다

2. flexible YUV buffers (CodecCapabilities#COLOR_FormatYUV420Flexible)

    getInput/outputImage(int) 를 사용함으로써 Bytebuffer 모드 뿐만 아니라 input/output Surface와 함께 사용가능합니다. 

3. other, specific formats

    일반적으로 ByteBuffer 모드에서만 사용되는 format입니다. 몇몇 color format들은 공급 업체마다 다릅니다. 다른 것들은 CodecCapabilities에 정의 되어있     습니다. 유연한 형식과 동등한 색상 형식의 경우 getInput/OutputImage(int)를 계속 사용할 수 있습니다. 
    
* 모든 비디오 코덱들은 LOLLIPOP_MR1 부터 flexible YUV 4:2:0 버퍼를 지원합니다. 

## 구형 디바이스에서 Raw Video ByteBuffer 접근하기

LOLLIPOP 및 이미지 지원하기전에 raw output buffer의 레이아웃을 이해하려면 **MediaFormat#KEY_STRIDE** 및 **MediaFormat#KEY_SLICE_HEIGHT** 출력형식 값을 사용해야합니다. 

> 일부 장치에서는 슬라이스 높이가 0으로 보급됩니다. 이는 슬라이스 높이가 프레임 높이와 같거나 슬라이스 높이가 일부 값에 정렬 된 프레임 높이 (일반적으로 2). 
> 불행히도 이 경우 실제 슬라이스 높이를 알려주는 표준적이고 간단한 방법은 없습니다. 또한 평면 형식의 U 평면의 수직 보폭도 지정되거나 정의되지 않지만 일반적으로 슬라이> 스 높이의 절반입니다.

**MediaFormat # KEY_WIDTH** 및 **MediaFormat # KEY_HEIGHT** 키는 비디오 프레임의 크기를 지정합니다. 그러나 대부분의 경우 비디오 (사진)는 비디오 프레임의 일부만 차지합니다. 이것은 'Crop Rectangle'으로 표시됩니다.

출력 형식에서 원시 출력 이미지의 Crop Rectangle을 가져오려면 다음 키를 사용해야합니다. 이러한 키가 없으면 비디오가 전체 비디오 프레임을 차지합니다. Crop Retangle은 MediaFormat # KEY_ROTATION을 적용하기 전에 출력 프레임의 컨텍스트에서 이해됩니다.

| Format Key    | Type    | Description                                             |
|---------------|---------|---------------------------------------------------------|
| "crop-left"   | Integer | The left-coordinate (x) of the crop rectangle           |
| "crop-top"    | Integer | The top-coordinate (y) of the crop rectangle            |
| "crop-right"  | Integer | The right-coordinate (x) MINUS 1 of the crop rectangle  |
| "crop-bottom" | Integer | The bottom-coordinate (y) MINUS 1 of the crop rectangle |

오른쪽 및 아래쪽 좌표는 잘린 출력 이미지의 가장 오른쪽에있는 유효한 열 / 맨 아래에있는 유효한 행의 좌표로 이해 될 수 있습니다.
회전하기 이전의 비디오 프레임의 사이즈는 다음과 같이 계산됩니다

~~~java
 MediaFormat format = decoder.getOutputFormat(…);
 int width = format.getInteger(MediaFormat.KEY_WIDTH);
 if (format.containsKey("crop-left") && format.containsKey("crop-right")) {
    width = format.getInteger("crop-right") + 1 - format.getInteger("crop-left");
 }
 int height = format.getInteger(MediaFormat.KEY_HEIGHT);
 if (format.containsKey("crop-top") && format.containsKey("crop-bottom")) {
    height = format.getInteger("crop-bottom") + 1 - format.getInteger("crop-top");
 }
~~~
