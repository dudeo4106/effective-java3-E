# ð ã³ã³ã¹ãã©ã¯ã¿ã«åªä»å¤æ°ãå¤ãå ´åã¯ãã«ãã¼ãèæ®ããªãã

> éçãã¡ã¯ããªã¼ã¨ã³ã³ã¹ãã©ã¯ã¿ã«ã¯é¸æåªä»å¤æ°ãå¤ãæãé©åã«å¯¾å¿ãã«ããã§ãã

<br>

## ð æ¹æ³â : ã³ã³ã¹ãã©ã¯ã¿ãä½¿ç¨

åªä»å¤æ°æ°ãå¤ããªãã¨ã¯ã©ã¤ã¢ã³ãã³ã¼ãã®ä½æãèª­ã¿è¾¼ã¿ãå°é£ã«ãªãã¾ãã

````
NutritionFacts cocaCola = new NutritionFacts(240, 8, 100, 0, 35, 27)
````

<br>

## ð æ¹æ³â¡: ã¸ã£ã¯ãã¼ã³ãºãã¿ã¼ã³ãä½¿ç¨

ä¾ã®ããã«ãJavbinsãã¿ã¼ã³ã§ã¯ãªãã¸ã§ã¯ããä¸ã¤ä½ãããã«ã¯ã¡ã½ãããè¤æ°å¼ã³åºããªããã°ãªããªãã<br>
ã¾ãããªãã¸ã§ã¯ããå®å¨ã«çæãããã¾ã§ã¯ä¸è²«æ§ãå´©ããç¶æã«ãªãã¾ãã

````
NutritionFacts cocaCola = new NutritionFacts()
cocaCola.setServingSize(240);
cocaCola.setServings(8);
cocaCola.setCalories(100);
cocaCola.setSodium(35);
cocaCola.setCarbohydrate(27);
````

<br>

## ð æ¹æ³â¢: ãã«ãã¼ãä½¿ç¨

å¿é åªä»å¤æ°ã ãã§ã³ã³ã¹ãã©ã¯ã¿ãå¼ã³åºãã¦ãã«ãã¼ãªãã¸ã§ã¯ããå¾ããã«ãã¼ãªãã¸ã§ã¯ããæä¾ããä¸ç¨®ã®ã»ãã¿ã¼ã¡ã½ããã«ãããå¸æããé¸æåªä»å¤æ°ãè¨­å®ãã¾ãã <br>
æå¾ã«ãåªä»å¤æ°ã®ãªãbuildã¡ã½ãããå¼ã³åºããæãã«å¿è¦ãªãªãã¸ã§ã¯ããåå¾ãã¾ãã
````
public class NutritionFacts {
    private final int servingSize;
    private final int servings;
    private final int calories;
    private final int fat;
    private final int sodium;
    private final int carbohydrate;

    public static class Builder {
        private final int servingSize;
        private final int servings;

        private final int calories = 0;
        private final int fat = 0;
        private final int sodium = 0;
        private final int carbohydrate = 0;

        public Builder Build(int servingSize, int servings) {
            this.servingSize = servingSize;
            this.servings = servings;
        }

        public Builder Build(int val) {
            this.calories = val;
            return this;
        }

        public Builder Build(int val) {
            this.fat = val;
            return this;
        }

        public Builder Build(int val) {
            this.sodium = val;
            return this;
        }

        public Builder Build(int val) {
            this.carbohydrate = val;
            return this;
        }

        public NutritionFacts(Builder builder) {
            return new NutritionFacts(this);
        }
    }
    
    private NutritionFacts(Builder builder) {
        return new NutritionFacts(this);
    }
}

NutritionFacts cocaCola = NutritionFacts.Builder(240, 8)
        .calories(100).sodium(35).carbohydrate(27).build();
````

<br>

## ð ç­æ

ç­æã¨ãã¦ã¯ããªãã¸ã§ã¯ããä½ãåã«ã¾ããã«ãã¼ãä½ããªããã°ãªãã¾ããããæ§è½ã«ææãªç¶æ³ã§ã¯ãã®ç¹ãåé¡ã«ãªãããããã¾ããã<br>
ããã¦ãã³ã³ã¹ãã©ã¯ã¿ãä½¿ç¨ãããããã³ã¼ããé·ãã§ãã å¾ã£ã¦ããã«ãã¼ãã¿ã¼ã³ã¯åªä»å¤æ°4ã¤ä»¥ä¸ã ã£ãããå°æ¥å¢ããå¯è½æ§ãããå ´åã«ä½¿ç¨ããæ¹ãè¯ãã§ãã

