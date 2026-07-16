# 單元 1 - Spring Boot 簡介

### Java 的三大特性

#### 繼承 (Inheritance)

> 「承襲既有的功能，並擴充新的特性。」
>

繼承允許一個新類別（子類別 / Subclass）繼承一個已存在類別（父類別 / Superclass）的屬性和方法。

使用 `extends` 關鍵字來實作繼承

#### 封裝 (Encapsulation)

> 「隱藏實作細節，只暴露操作介面。」
>

將類別（`Class`）的屬性（`Variables`）設為 `private`，防止外部程式直接修改。

提供公開的 `public` 方法（也就是 `Getter` **和** `Setter`）來存取與修改這些屬性

#### 多型 (Polymorphism)

> 「同一種宣告，多種不同的執行結果。」
>

要實現多型，通常需要滿足三個條件：

1. 有**繼承**或實作（`Implement`）關係。
2. 子類別覆寫（`Override`）父類別的方法。
3. 父類別的變數指向子類別的物件。

想像有一個父類別叫 `動物`，它有一個方法叫 `發出聲音()`。

當變數指向 `貓` 物件時，呼叫 `發出聲音()` 會輸出「喵喵」。

```java
動物 myCat = new 貓();
myCat.發出聲音(); // 輸出：喵喵
```

因為你用父類別去框住它，你只能透過父類別有的管道（介面）去操作它。而多型最神奇的地方，就在於雖然管道是舊的（動物），呼叫出來的效果卻是全新的（喵喵）

---

### Java 關鍵字

#### `public`（公開的）

**概念：** 毫無保留，對所有人開放。

**常見用途：** 供外部呼叫的方法（例如：Getter/Setter、主要商業邏輯介面）。

#### `private`（私有的）

**概念：** 高度機密，只有「自己人」能看。只有**定義該關鍵字的類別（Class）內部**可以存取

**常見用途：** 類別的屬性（Variables）。為了保護資料不被亂改，通常會設為 `private`，再透過 `public` 方法讓人在限制下存取。

#### `static`（靜態的）

**概念：** **屬於「類別」，而不屬於「個別物件」。**

**效果：**

沒加 `static` 的東西（Instance Member）：必須要 `new` 出物件後才能使用，每個物件各自獨立擁有一份。

加了 `static` 的東西（Class Member）：它在記憶體中**`只會存在一份`**，不需要 `new` 物件，直接用類別名稱就能呼叫。

**常見用途：** 工具類方法（例如：`Math.sqrt()`）、共用的計數器、全域設定值。

#### `final`（最終的）

**概念：** **一旦決定就不能再改變。**

最常見的終極組合：`public static final`

```java
public class GameConfig {
    // 定義一個全域、不可修改的系統常數
    public static final int MAX_PLAYERS = 4;
}
```

---

常用集合 (Collections)

- List（列表）：有序、可重複
- Set（集合）：無序、不可重複
- Map（映射）：鍵值對 (Key-Value)

```java
// List：有序、可重複
List<String> list = new ArrayList<>();
list.add("Apple");
list.add("Apple"); // 允許重複
System.out.println(list); // 輸出: [Apple, Apple]

// Set：無序、不可重複
Set<String> set = new HashSet<>();
set.add("Apple");
set.add("Apple"); // 重複的會被忽略
System.out.println(set); // 輸出: [Apple]

// Map：鍵值對
Map<String, Integer> map = new HashMap<>();
map.add("Apple", 10); // Key是"Apple", Value是 10
map.add("Banana", 20);
System.out.println(map.get("Apple")); // 輸出: 10
```
