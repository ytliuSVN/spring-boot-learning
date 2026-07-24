# 單元 10 - 取得請求參數（四）@PathVariable

去取得放在 url 路徑裡面的値

將 `@RequestMapping` 和 `@RequestParam` 這兩個註解融合在一起的感覺

### @PathVariable

- 用法：只能加在方法的參數上
- 用途：取得 url 路徑的値

> [http://localhost:8080/test4/123](http://localhost:8080/test4/123)
>

將 url 路徑 `/test4/{id}` 對應到 `test4` 方法上

```java
@RestController
public class MyController {

    @RequestMapping("/test4/{id}")
    public String test4(@PathVariable Integer id) {
        System.out.println("id: " + id);
        return "Hello test4";
    }
}

```

傳遞多個資訊 GET [http://localhost:8080/test4/123/judy](http://localhost:8080/test4/123/judy)

```java
@RestController
public class MyController {

    @RequestMapping("/test4/{id}/{name}")
    public String test4(@PathVariable Integer id,
                        @PathVariable String name) {
        System.out.println("id: " + id);
        System.out.println("name: " + name);
        return "Hello test4";
    }
}

```