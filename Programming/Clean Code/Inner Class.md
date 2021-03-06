## What are the purpose of inner classes ([StackOverFlow](https://stackoverflow.com/questions/11398122/what-are-the-purposes-of-inner-classes))

### Best Answer 
Inner Class 는 한 곳에서 논리적으로 그룹핑을 할 목적으로 사용하는 것이 베스트이다. 

#### Nested Class [Oracle Docs](https://docs.oracle.com/javase/tutorial/java/javaOO/nested.html)
: 자바 프로그래밍에서는 클래스 안에 다른 클래스를 정의하는 것을 허용한다.
Nested Classes 는 크게 static 과 non-static 으로 구분된다. 
static 은 static nested class 라고 불리고
non-static 은 inner class 라고 불린다. 

~~~java
class OuterClass {
    ...
    class NestedClass {
        ...
    }
}
~~~  

#### 사용하는 이유
1. 한 곳(한 파일)에서 사용되는 클래스들을 그룹핑하기 위한 방법 중 하나이다 
2. 캡슐화를 증대시킨다
3. 좀 더 가독성 있고 유지보수에 용이한 코드를 야기한다