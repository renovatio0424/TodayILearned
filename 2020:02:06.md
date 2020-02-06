# 2020/02/06

## Try Catch 로 OOM 을 잡을 수 있다? 

[reference](https://marlboroyw.tistory.com/481)

하다 보니 다른 곳에서 메모리 변경 되었을 경우에 대한 처리는 어떻게 할지 ... 

~~~ java
TestModel tm = new TestModel();
try {
  tem.generateOOM();
} catch (OutOfMemeoryError e) {
  Log.d(null,"oom !!!!!!!!!!!!!");
}
~~~
