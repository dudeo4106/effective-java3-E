# 🔑 생성자 대신 정적 팩터리 메서드를 고려하라

<br>

## 📌 장점 ①: 이름을 가질 수 있다.

생성자에 넘기는 매개변수와 생성자 자체만으로는 반환될 객체의 특성을 제대로 설명하지 못한다.<br>
그렇기에 팩토리 메소드를 사용하는 것이 코드를 읽기 편할 수 있다.
```
BigInteger.probablePrime
```
또한 한 클래스에 시그니처가 같은 생성자를 여러개 생성할 수 없다.<br>
이런 경우에는 생성자를 정적 팩터리 메서드로 바꾸고 각각의 차이를 잘 드러내는 이름을 지어주는 것이 좋다

<br>

## 📌 장점 ②: 호출될 때마다 인스턴스를 새로 생성하지는 않아도 된다.

불변 클래스는 인스턴스를 미리 만들어 놓거나, <br>
새로 생성한 인스턴스를 캐싱하여 재활용하기에 불필요한 객체 생성을 피할 수 있다.<br>
```
Boolean.valueOf(boolean)
```

<br>

## 📌 장점 ③: 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.

먼저 클래스에서 만들어 줄 객체의 클래스를 선택할 수 있게 하는 "엄청난 유연성"을 선물한다.<br>
API를 만들 때 이 유연성을 응용하면 구현 클래스를 공개하지 않고도 그 객체를 반환할 수 있어 API를 작게 유지 할 수 있다.
<br>
`java.util.Collections`는 45개 클래스를 공개하지 않기 때문에 API 외견을 훨씬 작게 만들 수 있었다.<br>
이 말은 인터페이스만으로 다루게 되는 것을 의미한다.<br>
프로그래머는 명시한 인터페이스대로 동작하는 객체를 얻을 것임을 알기에 굳이 별도 문서를 찾아가며 실제 구현 클래스가 무엇인지 알아보지 않아도된다.<br>
그렇기에 public으로 제공해야 할 API를 줄였을 뿐 아니라 개념적인 무게까지 줄 일 수 있었다.

<br>

## 📌 장점 ④: 리턴하는 객체의 클래스가 입력 매개변수에 따라 매번 다를 수 있다.

클라이언트는 팩터리가 건네주는 객체가 어느 클래스의 인스턴스인지 알 수도 없고 알 필요도 없다.<br>
예를 들어 OpenJDK에서 EnumSet는 원소가 64개 이하면 RegularEnumSet를 65개이상이면 JumboEnumSet의 인터턴스를 반환한다.<br>
이런 객체 타입은 노출되지 않기 때문에 추후 JDK의 변화에따라 새로운 타입을 만들거나 기존 타입을 없애도 문제가 되지 않는다.

<br>

## 📌 장점 ⑤: 정적 팩터리 메서드를 작성하는 시점에는 반환할 객체의 클래스가 존재하지 않아도 된다.

이러한 유연함은 서비스 제공자 프레임워크(Service Provider Framework)를 만드는 근간이되며 대표적으로 JDBC를 예로 한다.<br>
서비스 제공자 프레임워크는 3개의 핵심 컴포넌트로 이뤄진다.<br>
```
● 구현체의 동작을 정의하는 서비스 인터페이스
● 제공자가 구현체를 등록할 때 사용하는 제공자 등록 API
● 클라이언트가 서비스의 인스턴스를 얻을 때 사용하는 서비스 접근 API
```
부가적으로, 서비스 인터페이스의 인스턴스를 제공하는 서비스 프로바이더 인터페이스를 만들 수도 있는데 그게 없다면 리플랙션을 사용해서 구현체를 만들어준다<br>
<br>
JDBC에서는
<br>
```
● Connection이 서비스 인터페이스
● DriverManager.registerDriver()가 제공자 등록 API
● DriverManager.getConnection()이  서비스 접근 API
```
의 역할을 수행한다.<br>

자바 6부터는 java.util.ServiceLoader라는 일반적인 용도의 서비스 프로바이더를 제공하지만, JDBC가 그 보다 이전에 만들어졌기 때문에 JDBC는 ServiceLoader를 사용하진 않는다.

<br>

## 📌 단점 ①: 상속을 하려면 Public이나 Protected 생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다.

따라서, Collections 프레임워크에서 제공하는 편의성 구현체(java.util.Collections)는 상속할 수 없다. <br>
어찌 보면 이 제약은 상속보다 컴포지션을 사용 하도록 유도하고 불변 타입으로 만들려면 이 제약을 지켜야 한다는 점에서 오히려 장점으로 받아들일 수도 있다.

<br>

## 📌 단점 ②: 정적 팩터리 메서드는 프로그래머가 찾기 어렵다.

생성자는 Javadoc 상단에 모아서 보여주지만 static 팩토리 메소드는 API 문서에서 특별히 다뤄주지 않는다.<br>
따라서 클래스나 인터페이스 문서 상단에 팩토리 메소드에 대한 문서를 제공하는 것이 좋겠다.

<br>
