# 2020/06/23

## java.lang.RuntimeException: Unable to invoke no-args constructor for interface InterfaceName. Registering an InstanceCreator with Gson for this type may fix this problem.

### 발생하게 된 배경 
Gson으로 json string 을 object 로 변환하는 과정에서 아래의 exception 이 발생하였다

    java.lang.RuntimeException: Unable to invoke no-args constructor for interface InterfaceName. 
    Registering an InstanceCreator with Gson for this type may fix this problem.
    
Exception을 야기한 라인은 아래와 같다

~~~java
SomeClass someClass = Gson().fromJson(jsonString, someClass.class)
~~~
          
### 해결 과정
위 exception 을 검색하여 보았다.
[How To Serialize And Deserialize Interfaces In Java Using Gson](https://technology.finra.org/code/serialize-deserialize-interfaces-in-java.html) 을 요약하자면 
interface를 implement한 클래스를 역직렬화할 때에는 Gson 에서 해당 클래스를 식별할 방법이 없다고 한다. 
그렇기 때문에 Interface를 식별할 수 있도록 도와주는 Adapter를 구현을 해야한다고 한다. 

하지만 나의 경우에 의심이 들었던 것은 

기존에는 동작을 잘하던 라인이었는데 이번에 동작을 제대로 하지 않았다는 것이었다. 
그래서 최근에 변경된 사항을 확인을 하는데 원인이라고 추측되는 부분을 찾게 되었다. 

~~~kotlin 
//kotlin 
class SomeClass {
  val childClass1: ChildClassInterface = ChildClass(0, 100);
  val childClass2: ChildClassInterface = ChildClass(-100, 100);
  val childClass3: ChildClassInterface = ChildClass(-50, 50);
}

class ChildClass(
  min: Int, 
  max: Int) {

}

interface ChildClassInterface {

}
~~~

여기서 문제가 되었던 라인은 childClass1,2,3 의 타입을 ChildClassInterface로 적었던 부분이었다. 
이 부분이 문제가 되었던 이유는 (정확한지는 잘 모르겠지만 추측이다)

kotlin 파일을 decompile을 하면 아래처럼 보여진다 

~~~java
  ChildClassInterface childClass1 = (ChildClassInterface)(new ChildClass(0,100));
~~~

Type Casting 이 자동으로 되는 걸 볼 수 있다. 
즉 **Gson 입장에서는 childClass 가 어떤 클래스인지 명확히 알 수 없기 때문에** 
위와 같은 Exception을 발생시켰던 것 같다. 
그래서 Type 정의하는 부분을 삭제하니 제대로 동작하는 것을 확인하였다. 

~~~kotlin 
class SomeClass {
  val childClass1 = ChildClass(0, 100);
  val childClass2 = ChildClass(-100, 100);
  val childClass3 = ChildClass(-50, 50);
}
~~~
