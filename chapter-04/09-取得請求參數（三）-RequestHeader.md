# 單元 9 - 取得請求參數（三）@RequestHeader

任何 HTTP 方法在傳送 HTTP 請求時，都可以包含 Request Headers

### @RequestHeader 可使用的設定

- name（or value）：指定 request header 的 header 名字，譲我們可以順利地去取得到中間帯有 `-` 的那些 header

```java
@RestController
public class MyController {

    @RequestMapping("/test3")
    public String test3(@RequestHeader(name = "Content-Type") String contentType) {
        System.out.println("Content-Type: " + contentType); // Content-Type: application/json
        return "Hello test3";
    }
}
```

- required：是否是必須的 header？
    - 預設是 `true`，可以改成 `false`
- defaultValue: `required = false` 的加強版，提供預設値