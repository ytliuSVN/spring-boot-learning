# 單元 9 - Mock 測試 – Mockito

## Mock 測試

- 目的：避免為了測試某一個單元測試，而去構建了整個 bean 的 dependency
- 做法：創造一個假的 bean，去替換掉 Spring 容器中原有的 bean

```mermaid
flowchart LR
    A(["Bean A"])
    B(["Mock Bean B"])
    C["使用 Mock Bean 返回<br/>指定的結果，專注在<br/>測試 Bean A 的邏輯"]
    D["想要測試 Bean A<br/>的實作是否正確"]

    A --> B
    B --- C
    D --> A

    classDef bean fill:#DCE5F5,stroke:#5479B9,stroke-width:2px,color:#000
    classDef mock fill:#D3D3D3,stroke:#222,stroke-width:2px,color:#000
    classDef note fill:transparent,stroke:transparent,color:#D22
    classDef description fill:transparent,stroke:transparent,color:#5479B9

    class A bean
    class B mock
    class C note
    class D description

    linkStyle 1 stroke:transparent
```

## Mockito

