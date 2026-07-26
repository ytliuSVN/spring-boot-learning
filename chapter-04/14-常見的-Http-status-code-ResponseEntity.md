# 單元 14 - 常見的 Http status code + ResponseEntity<?>

### 2xx－成功

| Http 狀態碼 | 代表的意思 |
| --- | --- |
| 200 OK | 請求成功 |
| 201 Created | 請求成功且新的資源成功被創建，通常用在 POST 的 response |
| 202 Accepted | 請求已經接受，但尚未處理完成 |

### 3xx-重新導向

| Http 狀態碼 | 代表的意思 |
| --- | --- |
| 301 Moved Permanently | 永久性重新導向，新的 url 應放在 response header 的 "Location" 中返回，通常會用在網頁搬家上 |
| 302 Found | 臨時重新導向，新的臨時性的 url 應放在 response header 的 "Location" 中返回 |

### 4xx-前端請求錯誤

| Http 狀態碼 | 代表的意思 |
| --- | --- |
| 400 Bad Request | 前端的請求參數有錯誤（例如：前端傳給後端的參數名稱不同、請求的格式有問題） |
| 401 Unauthorized | 沒有通過身份驗證 |
| 403 Forbidden | 請求被後端拒絕，通常是權限不足導致的 |
| 404 Not Found | 網頁不存在，可能是資源被移走或是 url輸入錯誤 |

### 5xx-後端處理有問題

| Http 狀態碼 | 代表的意思 |
| --- | --- |
| 500 Internal Server Error | 後端在執行程式時發生錯誤，可能是程式內有 bug 導致的 |
| 503 Service Unavailable | 由於臨時維護或者流量太大，後端目前沒有辦法處理請求 |
| 504 Gateway Timeout | 請求超時 |

### ResponseEntity<?>

- 用法：作為方法的返回類型
- 用途：自定義回傳的 http response 的細節

```java
@RestController
public class MyController {

    @RequestMapping("/test")
    public ResponseEntity<String> test() {
        // http 的狀態碼變成 202
        return ResponseEntity.status(HttpStatus.ACCEPTED).body("Hello World");
    }
}
```

HttpStatus.ACCEPTED 按下 `command` 鍵，點選 `HttpStatus` 後可以查看 Enumeration of HTTP status codes.