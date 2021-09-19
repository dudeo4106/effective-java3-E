# 🔑 privateコンストラクタまたは列挙タイプでシングルトンであることを保証しなさい

クラスをシングルトンにすると、これを使用するクライアントのテストが難しくなる可能性があります。<br>
タイプをインターフェースで定義した後、そのインターフェースを具現化したシングルターンでなければ、シングルトンインスタンスを偽物（mock）具現に変えることができないからです。

シングルトンで作る方式は普通二つのうち一つです。
両方ともコンストラクタはprivateで隠しておいて、唯一のインスタンスにアクセスできる手段としてpublic staticメンバーを一つ用意しておきます。

<br>

## 📌 方法①: public staticメンバーがfinalフィールド
リフレクションAPIであるAccessibleObject.setAccessibleを使う方法を除けば、<br>
コンストラクタは初期化されたときに作られたインスタンスが全システムで一つしかないことが保障されます。
```
public class Elvis {
    public static final Elvis INSTANCE = new Elvis();
    private Elvis() { ... }
    
    public void leaveTheBuilding() { ... }
}
```
長所1: 当該クラスがシングルターンであることがAPIにはっきり示されます。(public static finalですので、絶対に他のオブジェクトを参照することはできない)<br>
長所2: 簡潔さが長所です。

<br>

## 📌 方法②: static ファクトリー方式のシングルトン
```
public class Elvis {
    private static final Elvis INSTANCE = new Elvis();
    private Elvis() { ... }
    public static Elvis getInstance() { return INSTANCE; }
    
    public void leaveTheBuilding() { ... }
}
```
長所1: APIを変えなくてもシングルトンでなく変更できる点<br>
長所2: 静的ファクトリーをジェネリック·シングルトン·ファクトリーにできる点<br>
長所3: 静的ファクトリーのメソッド参照をsupplierとして使用できる点(Elvis::getInstance → Supplier<Elvis>)<br>

<br>

## 📌 追加: Serialization
```
private Object readResolve() {
    return INSTANCE;
}
```
上記のいずれかの方式で作ったシングルトンクラスを直列化するには？<br>
すべてのインスタンスフィールドをtransientと宣言し、readResolve メソッドを提供しなければなりません。<br>
こうしないと、直列化されたインスタンスを逆直列化するたびに新しいインスタンスが作られます。

<br>

## 📌 方法③: 列挙タイプ方式のシングルトン - 本で述べる最も望ましい方法
```
public enum Elvis {
    INSTANCE;
    public void leaveTheBuilding() { ... }
}
```
長所:もっと簡潔で、追加努力なしに直列化でき、さらに非常に複雑な直列化状況やリフレクション攻撃でも第2のインスタンスが生じることを完璧に防いでくれます。
少し不自然に見えますが、ほとんどの状況では元素が一つしかない列挙タイプがシングルトンを作る最良の方法です。<br>
短所: ただし、列挙タイプ以外のクラスを相続しなければならない場合は、この方法は使用できません。（ただし、インタフェースは具現化できる。）

<br>