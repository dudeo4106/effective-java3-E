# 🔑 コンストラクタに媒介変数が多い場合はビルダーを考慮しなさい

> 静的ファクトリーとコンストラクタには選択媒介変数が多い時、適切に対応しにくいです。

<br>

## 📌 方法①: コンストラクタを使用

媒介変数数が多くなるとクライアントコードの作成や読み込みが困難になります。

````
NutritionFacts cocaCola = new NutritionFacts(240, 8, 100, 0, 35, 27)
````

<br>

## 📌 方法②: ジャワビーンズパターンを使用

例のように、Javbinsパターンではオブジェクトを一つ作るためにはメソッドを複数呼び出さなければならない。<br>
また、オブジェクトが完全に生成されるまでは一貫性が崩れた状態になります。

````
NutritionFacts cocaCola = new NutritionFacts()
cocaCola.setServingSize(240);
cocaCola.setServings(8);
cocaCola.setCalories(100);
cocaCola.setSodium(35);
cocaCola.setCarbohydrate(27);
````

<br>

## 📌 方法③: ビルダーを使用

必須媒介変数だけでコンストラクタを呼び出してビルダーオブジェクトを得、ビルダーオブジェクトが提供する一種のセッターメソッドにより、希望する選択媒介変数を設定します。 <br>
最後に、媒介変数のないbuildメソッドを呼び出し、我々に必要なオブジェクトを取得します。
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

## 📌 短所

短所としては、オブジェクトを作る前にまずビルダーを作らなければなりませんが、性能に敏感な状況ではその点が問題になるかもしれません。<br>
そして、コンストラクタを使用するよりもコードが長いです。 従って、ビルダーパターンは媒介変数4つ以上だったり、将来増える可能性がある場合に使用した方が良いです。

