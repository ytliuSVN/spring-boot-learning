# 單元 11 - 設計 RESTful API

### REST 風格

- 目的：簡化溝通成本
- 如果你所設計的 API 符合 REST 風格，那麽你所設計的 API 就是 RESTful API
    - Beauty - Beautiful
    - Peace -> Peaceful
- 使用 http method 表示動作
- 使用 url 路徑描述資源之間的階層關係

| Http method + url 路徑 | 說明 |
| --- | --- |
| GET /users | 取得所有 user |
| GET /users/123 | 取得 user id 為123的 user |
| GET /users/123/articles/456 | 取得 user id為123的user 所寫的、article id 為456的文章 |
| GET /users/123/videos | 取得 user id 為123的user 所錄的所有影片 |
- response body 返回 `json` 或是 `xml` 格式