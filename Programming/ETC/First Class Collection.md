
## First Class Collection [우아한 형제들](https://woowabros.github.io/techcourse/2020/06/05/techcourse-javable.html)

### 일급 콜렉션 언급 배경

[소트웍스 앤솔로지 객체지향 생활체조편]

> 규칙 8: 일급 콜렉션 사용
> 이 규칙의 적용은 간단하다.
> 콜렉션을 포함한 클래스는 반드시 다른 멤버 변수가 없어야 한다.
> 각 콜렉션은 그 자체로 포장돼 있으므로 이제 콜렉션과 관련된 동작은 근거지가 마련된셈이다.
> 필터가 이 새 클래스의 일부가 됨을 알 수 있다.
> 필터는 또한 스스로 함수 객체가 될 수 있다.
> 또한 새 클래스는 두 그룹을 같이 묶는다든가 그룹의 각 원소에 규칙을 적용하는 등의 동작을 처리할 수 있다.
> 이는 인스턴스 변수에 대한 규칙의 확실한 확장이지만 그 자체를 위해서도 중요하다.
> 콜렉션은 실로 매우 유용한 원시 타입이다.
> 많은 동작이 있지만 후임 프로그래머나 유지보수 담당자에 의미적 의도나 단초는 거의 없다.


### 일급 컬렉션이란?
~~~java
// example
public class Lotto {
    private final List<LottoNumber> lotto;
    // ...
    public List<LottoNumber> getLotto() {
        return lotto;
    }
}

//First Class Collection
public class Lotto {
    private final List<LottoNumber> lotto;

    public Lotto(List<LottoNumber> lotto) {
        this.lotto = lotto;
    }

    public List<LottoNumber> getLotto() {
        return lotto;
    }
}

public class LottoNumber {
    private final int lottoNumber;

    public LottoNumber(int lottoNumber) {
        this.lottoNumber = lottoNumber;
    }
    
    // toString()은 로그를 찍기 위함이다.
    @Override
    public String toString() {
        return "LottoNumber{" +
                "lottoNumber=" + lottoNumber +
                '}';
    }
}
~~~

### 일급 컬렉션의 이점
1. 비즈니스에 종속적인 자료구조
2. Collection의 불변성을 보장
3. 상태와 행위를 한 곳에서 관리
4. 이름이 있는 컬렉션

#### 비즈니스 종속적인 자료구조 
#### 컬렉션 불변성
final -> 재할당만



#### 컬렉션 