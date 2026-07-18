# 單元 3 - Bean 的注入 - @Autowired、@Qualifier

### @Autowired

- 用法：通常是加在 class 變數上
- 用途：根據變數的類型，去 Spring 容器中尋找有沒有符合類型的 bean

```java
@Component
public class Teacher {

		@Autowired
    private Printer printer; // 類型符合，注入成功
    // 變數的類型盡量使用 Interface

    public void teach() {
        printer.print("I'm a teacher");
    }
}
```

#### Spring 容器

```markdown
-----------------------------------------------------------------
|  Spring 容器 (Spring Container)                                |
|                                                               |
|    Printer hpPrinter = new HpPrinter();                       |
|   ---------                                                   |
|       |                                                       |
|       |                                                       |
|       v                                                       |
|   _______________________________________                     |
|  |                                       |                    |
|  |             Bean hpPrinter            |                    |
|  |_______________________________________|                    |
|                                                               |
-----------------------------------------------------------------
```

### @Qualifier

- 用法：通常是加在 class 變數上，會跟 `@Autowired` 一起用
- 用途：指定注入 Bean 的名字
- 註解寫法沒有順序性

```java
@Component
public class Teacher {

		@Autowired
		@Qualifier("hpPrinter")
    private Printer printer;

    public void teach() {
        printer.print("I'm a teacher");
    }
}
```
