# 單元 2 - Spring IoC 與 Bean

### IoC = Inversion of Control 控制反轉

- 將 object (物件) 的控制權，交給了外部的 Spring 容器 (Spring Container) 來管理。

```java
public class Teacher {

    private Printer printer;

    public void teach() {
        printer.print("I'm a teacher");
    }
}
```

### @Component

- 用法：只能加在 class 上
- 用途：將該 class 變成由 Spring 容器所管理的 object
- 被 Spring 容器創建的 object，叫做 Bean (`hpPrinter`)
- bean 的名字是由 class 的第一個字母轉成小寫

```java
@Component
public class HpPrinter implements Printer {

    @Override
    public void print(String message) {
        System.out.println("HP印表機: " + message);
    }
}
```

### DI (Dependency Injection)

將 Spring 容器所管理的 `hpPrinter` bean 去交到 `Teacher` 的手上:

1. 將 Teacher 也變為 bean, 加上 `@Component`
2. 在 printer 上面加上 `@Autowired` 註解

```java
@Component
public class Teacher {

    @Autowired
    private Printer printer;

    public void teach() {
        printer.print("I'm a teacher");
    }
}
```



### @RestController

```java
@RestController // 另一種可以創建 bean 的註解
public class MyController {

    @Autowired
    private Printer printer;

    @RequestMapping("/test")
    public String test() {
        printer.print("Hello World"); // HP印表機: Hello World
        return "Hello World";
    }
}
```



### Spring IoC 專有名詞

- IoC = Inversion of Control (控制反轉)
- DI = Dependency Injection (依賴注入)
- Bean = 存放在 Spring 容器內的 object
- `@Component` 註解 = 加在 class 上, 將該 class 變成 Spring 容器所管理的 bean
- `@Autowired` 註解 = 加在變數上, 取得 Spring 容器中的 bean

