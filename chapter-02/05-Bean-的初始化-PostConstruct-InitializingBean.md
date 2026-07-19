# 單元 5 - Bean 的初始化 - @PostConstruct、InitializingBean

初始化 Bean 的方法

1. 使用 `@PostConstruct`
2. 實現 `InitializingBean` interface 的 `afterPropertiesSet()` 方法
3. 兩個不要同時使用，擇一使用就好

### @PostConstruct

- 加上 `@PostConstruct` 註解的這個方法必須為 `public`
- 該方法的返回類型一定要是 `void`
- 方法名可以隨意取
- 不能有參數

```java
@Component
public class HpPrinter implements Printer {

    private int count;

    @PostConstruct
		public void initialize() {
		    count = 5;
		}

    @Override
    public void print(String message) {
        count--;
        System.out.println("HP 印表機: " + message);
        System.out.println("剩餘使用次數: " + count);
    }
}
```

### 實現 InitializingBean interface

```java
@Component
public class HpPrinter implements Printer, InitializingBean {

    private int count;

    @Override
    public void afterPropertiesSet() throw Exception {
		    count = 5;
    }

    @Override
    public void print(String message) {
        count--;
        System.out.println("HP 印表機: " + message);
        System.out.println("剩餘使用次數: " + count);
    }
}
```