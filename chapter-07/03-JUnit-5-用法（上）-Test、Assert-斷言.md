# 單元 3 - JUnit 5 用法（上） - @Test、Assert 斷言

# JUnit

* JUnit 是 Java 單元測試的必備工具
* 只要在方法上加上 `@Test`，即可生成一個單元測試

依據情況在 `pom.xml` 加上額外設定，禁用 JUnit 4

```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-test</artifactId>
    <scope>test</scope>
    <!--禁用 JUnit 4 的設定-->
    <exclusions>
        <exclusion>
            <groupId>org.junit.vintage</groupId>
            <artifactId>junit-vintage-engine</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

# JUnit 5 的用法

*  `@Test`：加在方法上，可以生成一個單元測試
* `@Test` 只能在 test 資料夾底下使用，可以將該方法變成可執行的 test case（測項）
* 方法為 `public void`，並且沒有任何參數
* 方法名稱可以隨意取，用來表達這個 test case 想測試哪個功能點，方法名稱是精華所在！

```java
public class CalculatorTest {

    @Test
    public void add() {
        Calculator calculator = new Calculator();
        int result = calculator.add(1, 2);

        assertEquals(3, result);
        // assertEquals(3, result, "計算結果が正しくありません。");
    }

    @Test
    public void divide() {
        Calculator calculator = new Calculator();
        int result = calculator.divide(4, 2);

        assertEquals(2, result);
    }
}
```

# JUnit 5 的 Assert 用法

若是不符合 assert 斷言的預期結果，則測試失敗

| Assert 系列用法 | 用途 |
| --- | --- |
| `assertNull(A)` | 斷言 A 為 null |
| `assertNotNull(A)` | 斷言 A 不為 null |
| `assertEquals(A, B)` | 斷言 A 和 B 相等，會使用 `equals()` 方法去判斷 |
| `assertTrue(A)` | 斷言 A 為 true |
| `assertFalse(A)` | 斷言 A 為 false |
| `assertThrows(exception, method)` | 斷言執行 method 時，會拋出 exception |


