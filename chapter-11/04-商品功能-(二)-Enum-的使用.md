# 單元 4 - 商品功能（二）- Enum 的使用

### constant

使用 全大寫 + 底線

```java
public enum ProductCategory {
    FOOD,
    CAR,
    E_BOOK
}
```

```java
public class MyTest {

    // shortcut: psvma
    static void main(String[] args) {
        ProductCategory category = ProductCategory.FOOD;
        String s = category.name();
        System.out.println(s); // FOOD

        String s2 = "CAR";
        ProductCategory category2 = ProductCategory.valueOf(s2);
        // ProductCategory.CAR
    }
}
```

Refactor → Type Migration

```java
public class Product {

    ...
    // private String category;
    private ProductCategory category;
```

回去修改 ProductRowMapper

```java
public class ProductRowMapper implements RowMapper<Product> {

    @Override
    public Product mapRow(ResultSet resultSet, int i)  throws SQLException {

        ...

        String categoryStr = resultSet.getString("category");
        ProductCategory category = ProductCategory.valueOf(categoryStr);
        product.setCategory(category);

        // product.setCategory(ProductCategory.valueOf(resultSet.getString("category")));

```