# 單元 4 - Bean 的創建 - @Component、@Configuration + @Bean

Bean 的創建方法

1. 在 Class 上加上 `@Component` 註解
2. 使用 `@Configuration` + `@Bean` 註解

### @Configuration

- 用法：只能加在 class 上
- 用途：Spring 中的設定用註解，表示這個 class 是拿來設定 Spring 用的

```java
@Configuration
public class MyConfiguration { // class 的名字不重要

    // do something
}
```

### @Bean

- 用法：只能加在帶有 @Configuration 的 class 裡面
- 用途：在 Spring 容器中創建一個 bean

```java
@Configuration
public class MyConfiguration { // class 的名字不重要

    @Bean
    public Printer myPrinter() {
		    return new HpPrinter();
    }
}
```

```java
-----------------------------------------------------------------
|  Spring 容器 (Spring Container)                                |
|                                                               |
|    Printer myPrinter = new 方法返回的 object = hpPrinter        |
|   ---------                                                   |
|       |                                                       |
|       |                                                       |
|       v                                                       |
|   _______________________________________                     |
|  |                                       |                    |
|  |             Bean myPrinter            |                    |
|  |_______________________________________|                    |
|                                                               |
-----------------------------------------------------------------
```

註解裡有字串，就優先當作 bean 的名字

```java
@Configuration
public class MyConfiguration { // class 的名字不重要

    @Bean("xxx")
    public Printer myPrinter() {
		    return new HpPrinter();
    }
}
```

```java
-----------------------------------------------------------------
|  Spring 容器 (Spring Container)                                |
|                                                               |
|    Printer xxx = 方法返回的 object                              |
|   ---------                                                   |
|       |                                                       |
|       |                                                       |
|       v                                                       |
|   _______________________________________                     |
|  |                                       |                    |
|  |             Bean xxx                  |                    |
|  |_______________________________________|                    |
|                                                               |
-----------------------------------------------------------------
```
