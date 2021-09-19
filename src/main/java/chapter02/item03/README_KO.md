# 🔑 private 생성자 또는 열거 타입으로 싱글턴임을 보증하라

> 클래스를 싱글턴으로 만들면 이를 사용하는 클라이언자를 테스트하기가 어려워질 수 있다.<br>
타입을 인터페이스로 정의한 다음 그 인터페이스를 구현해서 만든 싱글턴이 아니라면 싱글턴 인스턴스를 가짜(mock) 구현으로 대체할 수 없기 때문이다.

> 싱글턴으로 만드는 방식은 보통 둘 중 하나다. 
두 방식 모두 생성자는 private로 감춰두고, 유일한 인스턴스에 접근할 수 있는 수단으로 public static 멤버를 하나 마련해둔다.

<br>

## 📌 방법①: public static 멤버가 final 필드
리플렉션 API인 AccessibleObject.setAccessible을 사용하는 방법을 제외하면,<br>
생성자는 초기화 될 때 만들어진 인스턴스가 전체 시스템에서 하나뿐임이 보장된다.
```
public class Elvis {
    public static final Elvis INSTANCE = new Elvis();
    private Elvis() { ... }
    
    public void leaveTheBuilding() { ... }
}
```

장점1: 해당 클래스가 싱글턴임이 API에 명백히 드러난다.(public static final이니 절대로 다른 객체를 참조 할수 없음)<br>
장점2: 간결함이 장점이다.

<br>

## 📌 방법②: static 팩터리 방식의 싱글턴
```
public class Elvis {
    private static final Elvis INSTANCE = new Elvis();
    private Elvis() { ... }
    public static Elvis getInstance() { return INSTANCE; }
    
    public void leaveTheBuilding() { ... }
}
```
장점1: API를 바꾸지 않고도 싱글턴이 아니게 변경할 수 있다는 점<br>
장점2: 정적 팩터리를 제네릭 싱글턴 팩터리로 만들수 있다는 점<br>
장점3: 정적 팩터리의 메서드 참조를 supplier로 사용할 수 있다는 점(Elvis::getInstance → Supplier<Elvis>)<br>

<br>

## 📌 추가: 직렬화(Serialization)
```
private Object readResolve() {
    return INSTANCE;
}
```
위에 둘 중 하나의 방식으로 만든 싱글턴 클래스를 직렬화하려면?<br>
모든 인스턴스 필드를 transient라고 선언하고 readResolve메서드를 제공해야 한다.<br>
이렇게 하지 않으면 직렬화된 인스턴스를 역직렬화할 때마다 새로운 인스턴스가 만들어진다.

<br>

## 📌 방법③: 열거 타입 방식의 싱글턴 - 책에서 말하는 가장 바람직한 방법
```
public enum Elvis {
    INSTANCE;
    public void leaveTheBuilding() { ... }
}
```
장점: 더 간결하고, 추가 노력없이 직렬화 할 수 있고, 심지어 아주 복잡한 직렬화 상황이나 리플렉션 공격에서도 제2의 인스턴스가 생기는 일을 완벽히 막아준다.
조금 부자연스러워 보일 수느 있으나 대부분 상황에서는 원소가 하나뿐인 열거 타입이 싱글턴을 만드는 가장 좋은 방법이다.<br>
단점: 단 열거 타입외의 클래스를 상속해야 한다면 이 방법은 사용할 수 없다.(단 인터페이스는 구현한 수 있다.)

<br>