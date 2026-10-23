# 單元 4 - JUnit 5 用法（下） - @BeforeEach、@AfterEach、@BeforeAll、@AfterAll、@Disabled、@DisplayName

## JUnit 5 其他常用註解

* `@BeforeEach`、`@AfterEach`
  * `@BeforeEach`：在每次 `@Test` 開始前，都會執行一次
  * `@AfterEach`：在每次 `@Test` 結束後，都會執行一次

##  `@BeforeEach`、`@AfterEach`

```java
public class MyTest {

    @BeforeEach
    public void beforeEach() {
        System.out.println("執行 @BeforeEach");
    }

    @AfterEach
    public void afterEach() {
        System.out.println("執行 @AfterEach");
    }

    @Test
    public void test1() {
        System.out.println("執行 test1");
    }

    @Test
    public void test2() {
        System.out.println("執行 test2");
    }
}
```

運行結果

```
執行 @BeforeEach
執行 test1
執行 @AfterEach
執行 @BeforeEach
執行 test2
執行 @AfterEach
```

* `@BeforeAll`、`@AfterAll`
  * `@BeforeAll`：在所有 `@Test` 開始前執行一次
  * `@AfterAll`：在所有 `@Test` 結束後執行一次
  * 預設要求方法必須是 `static`
  * 實務上不常用，無法跟 Bean 做互動

##  `@BeforeAll`、`@AfterAll`

```java
public class MyTest {

    ...

    @BeforeAll
    public static void beforeAll() {
        System.out.println("執行 @BeforeAll");
    }

    @AfterAll
    public static void afterAll() {
        System.out.println("執行 @AfterAll");
    }

    @Test
    public void test1() {
        System.out.println("執行 test1");
    }

    @Test
    public void test2() {
        System.out.println("執行 test2");
    }
}
```

運行結果

```
執行 @BeforeAll
執行 @BeforeEach
執行 test1
執行 @AfterEach
執行 @BeforeEach
執行 test2
執行 @AfterEach
執行 @AfterAll
```

`@Disabled`：忽略該 `@Test` 不執行

```java
@Disabled
@Test
public void add() {
    ...
}
```


`@DisplayName`：自定義顯示名稱

```java
@DisplayName("割り算のテスト")
@Test
public void divide() {
    ...
}
```