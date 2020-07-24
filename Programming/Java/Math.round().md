## 소숫점 자리 관리 -> Math.round() [reference](https://coding-factory.tistory.com/250)

~~~java
double pie = 3.14159265358979;

System.out.println(Math.round(pie)); //결과 : 3
System.out.println(Math.round(pie*100)/100.0); //결과 : 3.14
System.out.println(Math.round(pie*1000)/1000.0); //결과 : 3.142
~~~
