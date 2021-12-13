# 🔑 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라

<br>

> 이하의 두 방식 모두 dictionary를 단 하나만 사용한다고 가정한다는 점에서 좋지 않다.

## 부적절한 구현 1 - 정적 유틸리티를 잘못 사용한 예

```
public class SpellChecker {
    private static final Lexicon dictionary = ...;

    private SpellChecker() {}

    public static boolean isValid(String word) { ... }
    public static List<String> suggestions(String typo) { ... }
}
```

<br>

## 부적절한 구현 2 - 싱글턴을 잘못 사용한 예

```
public class SpellChecker {
    private final Lexicon dictionary = ...;

    private SpellChecker(...) {}
    public static final SpellChecker INSTANCE = new SpellChecker(...);

    public boolean isValid(String word) { ... }
    public List<String> suggestions(String typo) { ... }
}
```

<br>

좋지 않은 이유로는 실전에서는 dictionary를 언어별로 따로 있고 특수 어휘용 dictionary를 별도로 두기도 한다. 심지어 테스트용 dictionary가 필요하다.<br>
final 한정자를 제거하고 다른 dictionary로 교체하는 메서드를 추가 할 수 있지만 이 방식은 오류를 내기 쉬우며 멀티스레드 환경에서 사용이 불가능 하다.<br>

## 적절한 구현 - 의존 객체 주입

```
public class SpellChecker {
    private final Lexicon dictionary;

    public SpellChecker(Lexicon dictionary) {
        this.dictionary = Objects.requireNonNull(dictionary);
    }

    public boolean isValid(String word) { ... }
    public List<String> suggestions(String typo) { ... }
}
```

위와 같이 여러 자원 인스턴스를 지원해야하며 클라이언트가 원하는 dictionary를 사용해야한다.<br>
이 조건을 만족하기 위해서는 인스턴스를 생성할 때 생성자에 필요한 자원을 넘겨주는 방식 즉 의존객체인 dictionary를 주입해주는 방법이다.



