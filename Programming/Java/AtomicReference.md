# 2020/02/05

## 1. AtomicReference (Java) [reference](http://tutorials.jenkov.com/java-util-concurrent/atomicreference.html)

1. 공부한 이유
: 비동기로 비트맵을 그리는 작업을 처리하는 중에 캐싱한 비트맵에 접근할 경우 lint에서 AtomicReference로 자동 변환해주어서 공부해봄

2. AtomicReference 클래스는 atomic하게 읽고 쓸 수 있는 object reference 변수를 제공함

    ** atomic : 원자, 즉, 쪼개어지거나, 따로따로 진행되어서는 안되는 것

~~~java
//creating
String initialReference = "the initially referenced string";
AtomicReference atomicReference = new AtomicReference(initialReference);

//getting
AtomicReference<String> atomicReference = new AtomicReference<String>("first value referenced");

String reference = atomicReference.get();

//setting
AtomicReference atomicReference = new AtomicReference();
    
atomicReference.set("New object referenced");

//comparing
String initialReference = "initial value referenced";

AtomicReference<String> atomicStringReference =new AtomicReference<String>(initialReference);

String newReference = "new value referenced";
boolean exchanged = atomicStringReference.compareAndSet(initialReference, newReference);
System.out.println("exchanged: " + exchanged);

exchanged = atomicStringReference.compareAndSet(initialReference, newReference);
System.out.println("exchanged: " + exchanged);
~~~
