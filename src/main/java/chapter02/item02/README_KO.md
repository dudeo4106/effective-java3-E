# π μμ±μμ λ§€κ°λ³μκ° λ§λ€λ©΄ λΉλλ₯Ό κ³ λ €νλΌ

> μ μ  ν©ν°λ¦¬μ μμ±μμλ μ νμ  λ§€κ°λ³μκ° λ§μ λ μ μ ν λμνκΈ° μ΄λ ΅λ€.

<br>

## π λ°©λ²β : μμ±μ μ¬μ©

λ§€κ°λ³μ κ°μκ° λ§μμ§λ©΄ ν΄λΌμ΄μΈνΈ μ½λλ₯Ό μμ±νκ±°λ μ½κΈ° μ΄λ ΅λ€.

````
NutritionFacts cocaCola = new NutritionFacts(240, 8, 100, 0, 35, 27)
````

<br>

## π λ°©λ²β‘: μλ°λΉμ¦ν¨ν΄ μ¬μ©

μμ μ²λΌ μλ°λΉμ¦ν¨ν΄μμλ κ°μ²΄ νλλ₯Ό λ§λ€λ €λ©΄ λ©μλλ₯Ό μ¬λ¬κ° νΈμΆν΄μΌνκ³ , κ°μ²΄κ° μμ ν μμ±λκΈ° μ κΉμ§λ μΌκ΄μ±μ΄ λ¬΄λμ§ μνμ λμ΄κ² λλ€.

````
NutritionFacts cocaCola = new NutritionFacts()
cocaCola.setServingSize(240);
cocaCola.setServings(8);
cocaCola.setCalories(100);
cocaCola.setSodium(35);
cocaCola.setCarbohydrate(27);
````

<br>

## π λ°©λ²β’: λΉλ μ¬μ©

νμ λ§€κ°λ³μλ§μΌλ‘ μμ±μλ₯Ό νΈμΆν΄ λΉλ κ°μ²΄λ₯Ό μ»κ³ , λΉλ κ°μ²΄κ° μ κ³΅νλ μΌμ’μ μΈν° λ©μλλ€λ‘ μνλ μ ν λ§€κ°λ³μλ€μ μ€μ . <br>
λ§μ§λ§μΌλ‘ λ§€κ°λ³μκ° μλ build λ©μλλ₯Ό νΈμΆν΄ μ°λ¦¬μκ² νμν κ°μ²΄λ₯Ό μ»λλ€.
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

## π λ¨μ 

λ¨μ μΌλ‘λ κ°μ²΄λ₯Ό λ§λ€κΈ° μ μ λ¨Όμ  λΉλλ₯Ό λ§λ€μ΄μΌ νλλ° μ±λ₯μ λ―Όκ°ν μν©μμλ κ·Έμ μ΄ λ¬Έμ κ° λ  μλ μλ€.<br> 
κ·Έλ¦¬κ³  μμ±μλ₯Ό μ¬μ©νλ κ²λ³΄λ€ μ½λκ° λ μ₯ν©νλ€. λ°λΌμ λΉλ ν¨ν΄μ λ§€κ°λ³μ 4κ° μ΄μμ΄κ±°λ μμΌλ‘ λμ΄λ  κ°λ₯μ±μ΄ μλ κ²½μ°μ μ¬μ©νλκ²μ΄ μ’λ€.

