# 單元 8 - 撰寫 Controller 層測試 (下) – MockMvc 的常用寫法

Builder 設計模式 (建造者模式)

```java
@Test
public void getById() throws Exception {
    // build request
    RequestBuilder requestBuilder = MockMvcRequestBuilders
            .get("/students/3");

    // send request and verify response
    mockMvc.perform(requestBuilder)
            .andDo(print())
            .andExpect(status().is(200))
            .andExpect(jsonPath("$.id").value(3))
            .andExpect(jsonPath("$.name").isNotEmpty());
}
```

[JSONPath Online Evaluator](https://jsonpath.com/)


### `andDo(print())`

將這次 HTTP Request 和 Response 的詳細資訊印出到 Console

```
MockHttpServletRequest:
      HTTP Method = GET
      Request URI = /students/3
       Parameters = {}
          Headers = []
             Body = null
    Session Attrs = {}

    ...

MockHttpServletResponse:
           Status = 200
    Error message = null
          Headers = [Content-Type:"application/json"]
     Content type = application/json
             Body = {"id":3,"name":"Judy","score":100.0,"graduate":true,"createDate":"2021-09-05T04:19:48.000+00:00"}
    Forwarded URL = null
   Redirected URL = null
```

### `andReturn()`

取得完整的執行結果。

```java
// send request and verify response
MvcResult mvcResult = mockMvc.perform(requestBuilder)
        .andDo(print())
        .andExpect(status().is(200))
        .andExpect(jsonPath("$.id").value(3))
        .andExpect(jsonPath("$.name").isNotEmpty())
        .andReturn();

String body = mvcResult.getResponse().getContentAsString();
System.out.println("response body: " + body);
```

```json
response body: {"id":3,"name":"Judy","score":100.0,"graduate":true,"createDate":"2021-09-05T04:19:48.000+00:00"}
```

模擬 API 發送帶有額外參數的 HTTP 請求。

```java
// build request
RequestBuilder requestBuilder = MockMvcRequestBuilders
        .get("/students/{studentId}", 3)
        .header("headerName", "headerValue")
        .queryParam("graduate", "true");
```

實際 URL 會變成：

```
GET /students/3?graduate=true
```
