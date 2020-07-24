## transient in Java ([Nesoy Blog](https://nesoy.github.io/articles/2018-06/Java-transient))

### transient 란?
    transient는 Serialize하는 과정에 제외하고 싶은 경우 선언하는 키워드입니다.
    
### Serialize 란?
    자바 시스템 내부에서 사용되는 Object 또는 Data를 외부의 자바 시스템에서도 사용할 수 있도록 byte 형태로 데이터를 변환하는 기술
    JVM(Java Virtual Machine 이하 JVM)의 메모리에 상주(힙 또는 스택)되어 있는 객체 데이터를 바이트 형태로 변환하는 기술
    
### Deserialize 란?
    byte로 변환된 Data를 원래대로 Object나 Data로 변환하는 기술을 역직렬화(Deserialize)라고 부릅니다.
    직렬화된 바이트 형태의 데이터를 객체로 변환해서 JVM으로 상주시키는 형태.