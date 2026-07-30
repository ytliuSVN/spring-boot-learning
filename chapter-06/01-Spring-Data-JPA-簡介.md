# 單元 1 - Spring Data JPA 簡介

### Spring JDBC

在 Spring Boot 中執行原始的 SQL 語法，去操作資料庫

### Spring Data JPA

使用 ORM 的概念，透過操作 Java object 的方式，去操作資料庫

### ORM

- Object-Relational Mapping (ORM)
- 用途：將 Java object，去對應到資料庫的 table，所以對 Java object 的操作，就是對資料庫的操作

### JPA

- 全稱為 Java Persistence API，定義要如何去操作資料庫
- JPA 提供了許多註解讓我們使用，像是 `@Entity`、`@Table`、`@Column`…

### Hibernate

- 一種 ORM 框架，去實現 JPA
- 負責自動生成 SQL 語法

### Spring JDBC vs Spring Data JPA

| **Spring JDBC** | **Spring Data JPA** |
| --- | --- |
| 以 SQL 為中心 | 以 Java Object 為中心 |
| 需要自己寫 SQL 語法，去操作資料庫 | 不需寫 SQL 語法，Hibernate 會自動生成 SQL 語法，去操作資料庫 |
| 開發效率較低 | 開發效率較高 |
| 效能較好 | 效能較差 |
| 可寫出複雜的 SQL 語法 | 很難寫出複雜的查詢 |
| 初期需要花一點時間上手，熟了之後就沒什麼問題 | 學習曲線易學難精 |