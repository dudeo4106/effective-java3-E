# 🔑 생성자에 매개변수가 많다면 빌더를 고려하라

> 정적 팩터리와 생성자에는 선택적 매개변수가 많을 때 적절히 대응하기 어렵다.<br>

<br>

## 📌 방법①: 생성자 사용

> 매개변수 개수가 많아지면 클라이언트 코드를 작성하거나 읽기 어렵다.

````
NutritionFacts cocaCola = new NutritionFacts(240, 8, 100, 0, 35, 27)
````

<br>

## 📌 방법②: 자바빈즈패턴 사용

> 예제처럼 자바빈즈패턴에서는 객체 하나를 만들려면 메서드를 여러개 호출해야하고, 객체가 오나전히 생성되기 전까지는 일관성이 무너진 상태에 놓이게 된다.

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

> 