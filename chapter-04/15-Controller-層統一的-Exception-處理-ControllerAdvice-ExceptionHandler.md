# 單元 15 - Controller 層統一的 Exception 處理 - @ControllerAdvice + @ExceptionHandler

Spring Boot 提供的功能

- `ResponseEntity<?>`：自定義每個方法所返回的 http response
- `@ControllerAdvice` + `@ExceptionHandler` : 自定義每個 Exception 所返回的 http response

### @ControllerAdvice

- 用法：只能加在 class 上
- 用途：將這個 class 變成一個 bean，並且可以在內部使用 `@ExceptionHandler`

### @ExceptionHandler

- 用法：只能加在方法上
- 用途：去 catch 方法所噴出的 Exception

使用 `@ControllerAdvice` 的好處 - 統一管理 Exception

底層由 SpringAOP 所實作

```java
@ControllerAdvice
public class MyExceptionHandler {

    @ExceptionHandler(RuntimeException.class)
    public ResponseEntity<String> handle(RuntimeException exception) {
        return ResponseEntity.status(HttpStatus.SERVICE_UNAVAILABLE) // 503
                .body("RuntimeException:" + exception.getMessage());
    }

    @ExceptionHandler(IllegalArgumentException.class)
    public ResponseEntity<String> handle(IllegalArgumentException exception) {
        return ResponseEntity.status(HttpStatus.BAD_REQUEST) // 400
                .body("IllegalArgumentException:" + exception.getMessage());
    }
}
```

```java
@RestController
public class MyController {

    @RequestMapping("/test1")
    public String test1() {
        throw new RuntimeException("text1 error");
    }

    @RequestMapping("/test2")
    public String test2() {
        throw new IllegalArgumentException("text2 error");
    }
}
```

滑鼠移到 IllegalArgumentException 按下 command 鍵，可查看繼承關係

```java
public class IllegalArgumentException extends RuntimeException {
```