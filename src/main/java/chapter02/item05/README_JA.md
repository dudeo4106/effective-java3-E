# 🔑 資源を直接明記せずに依存オブジェクト注入を使いなさい

<br>

> 以下の二つの方法とも、dictionary を一つだけ使用すると仮定する点では良くないです。

## 不適切な実装 1 - 静的ユーティリティを誤って使用した例

```
public class SpellChecker {
    private static final Lexicon dictionary = ...;

    private SpellChecker() {}

    public static boolean isValid(String word) { ... }
    public static List<String> suggestions(String typo) { ... }
}
```

<br>

## 不適切な実装 2 - シングルトンを誤って使用した例

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

良くない理由として、実戦ではdictionaryを言語別に、特殊語彙用dictionaryも別途に置くことがあります。 場合によってはテスト用のdictionaryまで必要です。<br>
final限定子を削除して他のdictionaryに交換するメソッドも追加できますが、この方法はエラーを出しやすく、マルチスレッド環境では使用できません。<br>

<br>

## 適切な実装 - 依存オブジェクト注入

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

上記のように複数の資源インスタンスをサポートし、クライアントが望むdictionaryを使用しなければなりません。<br>
この条件を満足させるためには、インスタンスを作成するときに、コンストラクタに必要な資源を渡す方法、つまり依存オブジェクトであるdictionaryを注入する方法です。<br>
この方法は資源が何個であれ依存関係がどうであれ、よく作動し、不変を保障して、多くのクライアントが依存オブジェクトを安心して共有できます。

```
Mosaic create(Supplier<? extends Tile> tileFactory) { ... }
```

この表現の使い道の変更はファクトリーメソッドパターンです。<br>
Java8で紹介したSupplier<T>インタフェースがファクトリーを表現した完璧な例であり、上記を参考にします。

ですが、依存オブジェクト注入が柔軟性とテストの容易性を改善してくれますが、依存性が数千にもなる大きなプロジェクトではコードを混乱させたりもします。<br>
このようなときは、スプリングなどの依存オブジェクト注入フレームワークを積極的に活用して、この乱れを解消するとよいでしょう。