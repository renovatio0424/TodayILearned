# 2020/07/15

## [Kotlin 1.4-M3 Preview](https://blog.jetbrains.com/kotlin/2020/07/kotlin-1-4-m3-is-out-standard-library-changes/)

### <fun interface>

  이제 Kotlin interface에도 SAM Conversion을 지원합니다. 
  사용할 때는 fun 키워드를 interface 앞에 붙여주셔야 합니다.

### <Collection operations>

    1. sumOf -> 비교값을 직접 정할 수 있습니다.
    2. max, min -> maxOrNull, minOrNull 로 이름이 변경됩니다.
    3. maxOf, minOf -> 비교값을 직접 정할 수 있습니다.
    4. Comparator를 인자로 받는 maxOfWith, minOfWith도 함께 추가됩니다.
    5. flatMap, flatMapTo가 다른 타입으로 변환하는 것을 추가로 허용합니다.
    6. Sequence에서 Iterable/Array/Map으로, Iterable에서 Sequence로 변경 가능해집니다.
    7. flatMapIndexed가 추가됩니다.

### <Common @Throws annotation>

    플랫폼 별로 다르게 사용했던 것을 공용으로 통합했습니다. 😉
  ~~~kotlin
  - kotlin.jvm.Throws
  - kotlin.native.Throws
  + kotlin.Throws
  ~~~

### <부동 소수점 배열에서의 비교>

    IEEE 754 표준에 따르면, NaN은 NaN과 동일하지 않아야 합니다.
    이런 이유로 DoubleArray 등에서 의도치 않은 결과가 발생하기도 합니다.
  
  ~~~kotlin
  val darray = doubleArrayOf(Double.NaN, 0.0)
  println(darray.contains(darray[0])) // false!
  ~~~

    이에 대한 대응으로 부동소수점 배열에서는 비교 함수가 더 이상 사용되지 않도록 contains/indexOf/lastIndexOf 확장함수가 deprecated 됩니다.

### <KType에서 Java Type으로의 변환>

    1.3.40 버전에서 소개된 typeOf에, Java Reflection 객체로 변환하는 기능이 추가되었습니다. Java 코드와 호환이 필요할 때 유용할 것 같습니다.

  ~~~kotlin
  val kType = typeOf<String>() // kotlin.String
  kType.javaType               // java.lang.String
  ~~~
  
  
## Why Android's indonesia language code is "in"?

- 인도네시아 언어 코드가 표준 문서와 달라 스트레스 받는 동료를 봄
- 그래서 구글 공식 문서를 확인해보니 다음의 글을 확인할 수 있었음

    >- ISO 639 is not a stable standard; some of the language codes it defines (specifically "iw", "ji", and "in") have changed. This constructor accepts both the old codes ("iw", "ji", and "in") and the new codes ("he", "yi", and "id"), but all other API on Locale will return only the OLD codes.
    >- For backward compatibility reasons, this constructor does not make any syntactic checks on the input.
    >- The two cases ("ja", "JP", "JP") and ("th", "TH", "TH") are handled specially, see Special Cases for more information.

- 여기서 나의 생각은 New Code 를 주는 API 는 없는건가 라는 생각이 들었음. 그래서 찾아낸 [API Document](https://developer.android.com/reference/java/util/Locale#toLanguageTag())
    ~~~kotlin
    Locale().toLanguageTag()
    ~~~
    
- Speacial Conversions section 을 확인해 보면 
    >- Deprecated ISO language codes "iw", "ji", and "in" are converted to "he", "yi", and "id", respectively.
    >- A locale with language "no", country "NO", and variant "NY", representing Norwegian Nynorsk (Norway), is converted to a language tag "nn-NO".
    
- 그래서 이 API 를 사용해서 해결했다!



