# 2020/03/03

## ConcurrentModificationException [(reference)](https://imasoftwareengineer.tistory.com/85)
이 예외는 어떤 스레드가 Iterrator 가 반복중인 Collection을 수정하는 경우 발생한다. 
어떤 쓰레드는 현재 반복문이 실행하고 있는 쓰레드일 수도 있고, 전혀 다른 쓰레드일 수도 있다. 

~~~java
public class Main {
    public static void main(String[] args) {
        List<Integer> list = new ArrayList<>();
        list.add(1);
        list.add(2);
        list.add(3);
        list.add(4);
        
        for(Integer i : list) {
            list.remove(i);
        }
    }
}

Exception in thread "main" java.util.ConcurrentModificationException
	at java.util.ArrayList$Itr.checkForComodification(ArrayList.java:909)
	at java.util.ArrayList$Itr.next(ArrayList.java:859)
	at Main.main(Main.java:14)


출처: https://imasoftwareengineer.tistory.com/85 [삐멜 소프트웨어 엔지니어]
~~~

해결 방법

1. for(;;) loop

~~~java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);

for(int i = 0; i < list.size(); i++) {
  if( i == 1 ) {
    list.remove(i);
  }
  System.out.println("인덱스: " + i + " - 값:" + list.get(i));
}
~~~
2. CopyOnWriteArray

~~~java
List<Integer> list = new CopyOnWriteArrayList<>();
list.add(1);
list.add(2);
list.add(3);

for(Integer i : list) {
  System.out.println("값:" + i);
  if( i == 2) {
    list.remove(i);
  }
}
~~~
3. 나중에 하기

~~~java
List<Integer> list = new ArrayList<>();
list.add(1);
list.add(2);
list.add(3);
list.add(4);
List<Integer> toRemove = new ArrayList<>();

for (Integer i : list) {
  if (i == 2) {
    toRemove.add(i);
  }
  System.out.println("값:" + i);
}

list.removeAll(toRemove);
System.out.println("--------");
for (Integer i : list) {
  System.out.println("값:" + i);
}
~~~
