# ð è³æºãç´æ¥æè¨ããã«ä¾å­ãªãã¸ã§ã¯ãæ³¨å¥ãä½¿ããªãã

<br>

> ä»¥ä¸ã®äºã¤ã®æ¹æ³ã¨ããdictionary ãä¸ã¤ã ãä½¿ç¨ããã¨ä»®å®ããç¹ã§ã¯è¯ããªãã§ãã

## ä¸é©åãªå®è£ 1 - éçã¦ã¼ãã£ãªãã£ãèª¤ã£ã¦ä½¿ç¨ããä¾

```
public class SpellChecker {
    private static final Lexicon dictionary = ...;

    private SpellChecker() {}

    public static boolean isValid(String word) { ... }
    public static List<String> suggestions(String typo) { ... }
}
```

<br>

## ä¸é©åãªå®è£ 2 - ã·ã³ã°ã«ãã³ãèª¤ã£ã¦ä½¿ç¨ããä¾

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

è¯ããªãçç±ã¨ãã¦ãå®æ¦ã§ã¯dictionaryãè¨èªå¥ã«ãç¹æ®èªå½ç¨dictionaryãå¥éã«ç½®ããã¨ãããã¾ãã å ´åã«ãã£ã¦ã¯ãã¹ãç¨ã®dictionaryã¾ã§å¿è¦ã§ãã<br>
finaléå®å­ãåé¤ãã¦ä»ã®dictionaryã«äº¤æããã¡ã½ãããè¿½å ã§ãã¾ããããã®æ¹æ³ã¯ã¨ã©ã¼ãåºããããããã«ãã¹ã¬ããç°å¢ã§ã¯ä½¿ç¨ã§ãã¾ããã<br>

<br>

## é©åãªå®è£ - ä¾å­ãªãã¸ã§ã¯ãæ³¨å¥

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

ä¸è¨ã®ããã«è¤æ°ã®è³æºã¤ã³ã¹ã¿ã³ã¹ããµãã¼ãããã¯ã©ã¤ã¢ã³ããæãdictionaryãä½¿ç¨ããªããã°ãªãã¾ããã<br>
ãã®æ¡ä»¶ãæºè¶³ãããããã«ã¯ãã¤ã³ã¹ã¿ã³ã¹ãä½æããã¨ãã«ãã³ã³ã¹ãã©ã¯ã¿ã«å¿è¦ãªè³æºãæ¸¡ãæ¹æ³ãã¤ã¾ãä¾å­ãªãã¸ã§ã¯ãã§ããdictionaryãæ³¨å¥ããæ¹æ³ã§ãã<br>
ãã®æ¹æ³ã¯è³æºãä½åã§ããä¾å­é¢ä¿ãã©ãã§ãããããä½åããä¸å¤ãä¿éãã¦ãå¤ãã®ã¯ã©ã¤ã¢ã³ããä¾å­ãªãã¸ã§ã¯ããå®å¿ãã¦å±æã§ãã¾ãã

```
Mosaic create(Supplier<? extends Tile> tileFactory) { ... }
```

ãã®è¡¨ç¾ã®ä½¿ãéã®å¤æ´ã¯ãã¡ã¯ããªã¼ã¡ã½ãããã¿ã¼ã³ã§ãã<br>
Java8ã§ç´¹ä»ããSupplier<T>ã¤ã³ã¿ãã§ã¼ã¹ããã¡ã¯ããªã¼ãè¡¨ç¾ããå®ç§ãªä¾ã§ãããä¸è¨ãåèã«ãã¾ãã

ã§ãããä¾å­ãªãã¸ã§ã¯ãæ³¨å¥ãæè»æ§ã¨ãã¹ãã®å®¹ææ§ãæ¹åãã¦ããã¾ãããä¾å­æ§ãæ°åã«ããªãå¤§ããªãã­ã¸ã§ã¯ãã§ã¯ã³ã¼ããæ··ä¹±ããããããã¾ãã<br>
ãã®ãããªã¨ãã¯ãã¹ããªã³ã°ãªã©ã®ä¾å­ãªãã¸ã§ã¯ãæ³¨å¥ãã¬ã¼ã ã¯ã¼ã¯ãç©æ¥µçã«æ´»ç¨ãã¦ããã®ä¹±ããè§£æ¶ããã¨ããã§ãããã