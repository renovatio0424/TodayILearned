## ConcurrentModificationException ([Android Developer](https://developer.android.com/reference/kotlin/java/util/ConcurrentModificationException))

### 발생 원인 
: 객체의 동시 수정이 허용되지 않았는데 수정을 할 때 메소드에 의해 발생합니다. 

### 발생하는 경우 
1. 한 스레드가 콜렉션을 수정하는 동안 다른 스레드가 반복적으로 콜렉션을 수정하는 경우
2. 단일 스레드에서 반복자를 사용하여 반복하는 동안 스레드가 직접 콜렉션을 수정하는 경우 
