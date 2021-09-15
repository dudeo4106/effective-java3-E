# 🔑 생성자에 매개변수가 많다면 빌더를 고려하라

> 정적 팩터리와 생성자에는 선택적 매개변수가 많을 때 적절히 대응하기 어렵다.<br>

<br>

## 📌 방법①: 생성자 사용

매개변수 개수가 많아지면 클라이언트 코드를 작성하거나 읽기 어렵다.

````
NutritionFacts cocaCola = new NutritionFacts(240, 8, 100, 0, 35, 27)
````

<br>

## 📌 방법②: 자바빈즈패턴 사용

예제처럼 자바빈즈패턴에서는 객체 하나를 만들려면 메서드를 여러개 호출해야하고, 객체가 오나전히 생성되기 전까지는 일관성이 무너진 상태에 놓이게 된다.

````
NutritionFacts cocaCola = new NutritionFacts()
cocaCola.setServingSize(240);
cocaCola.setServings(8);
cocaCola.setCalories(100);
cocaCola.setSodium(35);
cocaCola.setCarbohydrate(27);
````

<br>

## 📌 방법③: 빌더 사용

필수 매개변수만으로 생성자를 호출해 빌더 객체를 얻고, 빌더 객체가 제공하는 일조으이 세터 메서드들로 원하는 선택 매개변수들을 설정. <br>
마지막으로 매개변수가 없는 build 메서드를 호출해 우리에게 필요한 객체를 얻는다.
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

## 📌 단점

단점으로는 객체를 만들기 전에 먼저 빌더를 만들어야 하는데 성능에 민감한 상황에서는 그점이 문제가 될 수도 있다.<br> 
그리고 생성자를 사용하는 것보다 코드가 더 장황하다. 따라서 빌더 패턴은 매개변수 4개 이상이거나 앞으로 늘어날 가능성이 있는 경우에 사용하는것이 좋다.

