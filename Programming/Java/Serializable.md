# 2020/06/24

## Serializable

([oracle](https://docs.oracle.com/javase/7/docs/api/java/io/Serializable.html))

클래스에 `java.io.Serializable interface` 가 구현이 되면 Serialization 이 가능하다
이 인터페이스가 구현이 되지 않은 클래스는 어떤 상태에서든 직렬화 or 역직렬화가 되지 않는다 
serializable class 의 하위 타입에서는 자동으로 직렬화가 된다.
직렬화 인터페이스는 함수들과 필드들을 가지고 있지 않고 오직 직렬화 된 의미만 식별할 수 있도록 제공한다
직렬화 되지 않은 클래스의 하위 타입들에게 직렬화가 가능하도록 하려면, 하위타입은 아마 supertype 의 public, protected, (접근 가능하다면) package fields 들의 상태들을 복원하고 저장할 책임을 질 수 있다. 
하위 유형은 확장되는 클래스에 클래스 상태를 초기화할 수 있는 접근 가능한 no-arg 생성자가 있는 경우에만 이러한 책임을 질 수 있다.
그렇지 않은 경우 직렬화할 수 있는 클래스를 선언하는 것은 오류입니다. 런타임에 오류가 탐지됩니다.
역직렬화 중에 직렬화할 수 없는 클래스의 필드는 클래스의 공용 또는 보호된 no-arg 생성자를 사용하여 초기화됩니다. 직렬화할 수 있는 하위 클래스에 대해 no-arg 생성자에 액세스할 수 있어야 합니다. 
스트림에서 직렬화할 수 있는 하위 클래스의 필드가 복원됩니다.
그래프를 통과할 때 직렬화 가능 인터페이스를 지원하지 않는 객체가 나타날 수 있습니다. 이 경우 `NotSerializableException`이 발생하고 직렬화할 수 없는 객체의 클래스를 식별합니다.
직렬화 및 역직렬화 프로세스 중에 특수 처리가 필요한 클래스는 다음과 같은 정확한 서명을 사용하여 특수 메서드를 구현해야 합니다.

~~~java
 private void writeObject(java.io.ObjectOutputStream out)
     throws IOException
 private void readObject(java.io.ObjectInputStream in)
     throws IOException, ClassNotFoundException;
 private void readObjectNoData()
     throws ObjectStreamException;
~~~

`writeObject` 메서드는 해당 `readObject` 메서드가 복원할 수 있도록 특정 클래스에 대한 개체 상태를 쓰는 역할을 합니다.
오브젝트의 필드를 저장하기 위한 기본 메커니즘은 `out.defaultWriteObject` 호출하여 invoke할 수 있습니다.
이 방법은 슈퍼클래스 또는 서브클래스에 속하는 상태와 관련이 없습니다.
상태는 writeObject 메서드를 사용하여 ObjectOutputStream에 개별 필드를 쓰거나 DataOutput에서 지원하는 원시 데이터 유형에 대한 메서드를 사용하여 저장됩니다.

`readObject` 메서드는 스트림에서 읽고 클래스 필드를 복원하는 역할을 합니다. 객체의 non-static 및 non-transient 필드를 복원하기 위한 기본 메커니즘을 호출하기 위해 out.defaultReadObject를 호출할 수 있습니다. `defaultReadObject` 메서드는 스트림의 정보를 사용하여 스트림에 저장된 개체의 필드를 현재 개체에 해당하는 이름의 필드와 함께 할당합니다. 이렇게 하면 클래스가 새 필드를 추가하도록 진화한 사례가 처리됩니다. 이 방법은 슈퍼클래스 또는 서브클래스에 속하는 상태와 관련이 없습니다. 상태는 `writeObject` 메서드를 사용하여 ObjectOutputStream에 개별 필드를 쓰거나 DataOutput에서 지원하는 원시 데이터 유형에 대한 메서드를 사용하여 저장됩니다.

`readObjectNoData` 메서드는 직렬화 스트림이 지정된 클래스를 역직렬화할 개체의 수퍼클래스로 나열 하지 않는 경우 해당 클래스에 대한 개체의 상태를 초기화하는 역할을 합니다. 수신자가 발신자와 다른 버전의 역직렬화된 인스턴스의 클래스를 사용하고 수신자의 버전은 발신자의 버전에 의해 확장되지 않는 클래스를 확장하는 경우에 이러한 현상이 발생할 수 있습니다. 이 문제는 직렬화 스트림이 변조된 경우에도 발생할 수 있으므로 readObjectNoData는 "hostile" 또는 불완전한 소스 스트림에도 불구하고 역직렬화된 개체를 올바르게 초기화하는 데 유용합니다.

스트림에 개체를 쓸 때 사용할 대체 개체를 지정해야 하는 직렬화 가능 클래스는 다음 서명을 사용하여 특수 메소드를 구현해야 합니다.
~~~java
 ANY-ACCESS-MODIFIER Object writeReplace() throws ObjectStreamException;
~~~

이 `writeReplace` 메서드는 메서드가 존재하고 직렬화할 개체의 클래스 내에 정의된 메서드에서 액세스할 수 있는 경우 직렬화에 의해 호출됩니다. 따라서 이 메서드는 비공개, 보호 및 패키지-개인 액세스를 가질 수 있습니다. 이 메서드에 대한 하위 클래스 액세스는 Java 내게 필요한 옵션 규칙을 따릅니다.

스트림에서 해당 인스턴스를 읽을 때 교체를 지정해야 하는 클래스는 이 특수 방법을 정확한 서명으로 구현해야 합니다.
~~~java
 ANY-ACCESS-MODIFIER Object readResolve() throws ObjectStreamException;
~~~

이 `readResolve` 메서드는 `writeReplace`와 동일한 호출 규칙 및 내게 필요한 옵션 규칙을 따릅니다.

직렬화 런타임은 `serialVersion`이라고 하는 각 직렬화 가능 클래스와 버전 번호를 연결합니다.직렬화된 개체의 보낸 사람과 수신기가 직렬화와 관련하여 호환되는 클래스를 로드했는지 확인하는 데 사용되는 UID입니다. 수신기가 `serialVersion`이 다른 객체의 클래스를 로드한 경우입니다.해당 발송인 클래스의 UID보다 높은 UID를 지정하면 역직렬화로 인해 `InvalidClassException`이 발생합니다. 직렬화할 수 있는 클래스는 자체 `serialVersionUID`을 선언할 수 있습니다. `serialVersionUID` 필드를 선언하여 UID를 명시적으로 지정합니다. UID는 static, final, type long 이어야 합니다.

~~~java
 ANY-ACCESS-MODIFIER static final long serialVersionUID = 42L;
~~~

직렬화 가능 클래스가 serialVersion을 명시적으로 선언하지 않는 경우 serialVersion을 선언합니다.그러면 직렬화 런타임에 기본 serialVersion이 계산됩니다.Java(TM) 개체 일련화 규격에 설명된 대로 클래스의 다양한 측면을 기준으로 해당 클래스에 대한 UID 값입니다. 그러나 모든 직렬화 가능 클래스는 serialVersion을 명시적으로 선언하는 것이 좋습니다.기본 serialVersion 이후의 UID 값입니다.UID 계산은 컴파일러 구현에 따라 달라질 수 있는 클래스 세부 정보에 매우 민감하므로 역직렬화 중에 예기치 않은 InvalidClassExceptions가 발생할 수 있습니다. 따라서 serialVersion의 일관성을 보장합니다.서로 다른 Java 컴파일러 구현의 UID 값, 직렬화할 수 있는 클래스는 명시적 serialVersion을 선언해야 합니다.UID 값입니다. 명시적 serialVersion도 권장됩니다.UID 선언은 즉시 선언하는 class-serialVersion에만 적용되므로 가능한 경우 개인 한정자를 사용합니다.UID 필드는 상속된 구성원으로 유용하지 않습니다. 어레이 클래스가 명시적 serialVersion을 선언할 수 없습니다.UID는 항상 기본 계산 값을 가지지만 serialVersion을 일치시키기 위한 요구 사항입니다.어레이 클래스에 대해 UID 값이 무시됩니다.


Json String => Object ?
