# 單元 1 - Spring IoC 簡介

### Interface

```java
// Printer 的 interface, 裡面只有一個方法 (print) 去印東西
public interface Printer {
    void print(String message);
}
```



寫一個 class 去 implement 這個 interface

```java
// HpPrinter 的 class
public class HpPrinter implements Printer {

    @Override
    public void print(String message) {
        System.out.println("HP印表機: " + message);
    }
}

// 或是另一個 Canon 牌子的印表機
public class CanonPrinter implements Printer {

    @Override
    public void print(String message) {
        System.out.println("Canon印表機: " + message);
    }
}
```



設計一個 Teacher 跟 Student 的 class

- Interface
- 多型 (Polymorphism): 同一種宣告，多種不同的執行結果

```java
// Teacher class
public class Teacher {

    private Printer printer = new HpPrinter();
    // private Printer printer = new CanonPrinter();

    public void teach() {
		    // 呼叫的是 HpPrinter 裡面 @Override 的 print()
        printer.print("I'm a teacher");
    }
}

// Student class
public class Student {

    private Printer printer = new HpPrinter();
    // private Printer printer = new CanonPrinter();

    public void learn() {
		    // 呼叫的是 HpPrinter 裡面 @Override 的 print()
        printer.print("I'm a student");
    }
}
```



### IoC = Inversion of Control 控制反轉

- 將 object (物件) 的控制權，交給了外部的 Spring 容器 (Spring Container) 來管理。
- Loose coupling 鬆耦合，降低各個 class 之間的關聯性。
- Lifecycle Management 生命週期管理
- More testable 方便測試程式

```java
public class Teacher {

    private Printer printer;

    public void teach() {
        printer.print("I'm a teacher");
    }
}

public class Student {

    private Printer printer;

    public void learn() {
        printer.print("I'm a student");
    }
}
```

