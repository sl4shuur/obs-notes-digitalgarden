---
{"dg-publish":true,"permalink":"/hello/","created":"2025-01-31T22:24:55.224+02:00","updated":"2025-01-31T23:07:41.804+02:00"}
---

# hello
---

![Truth Table.png](/img/user/assets/img/Truth%20Table.png)

```mermaid
classDiagram
    Car *-- Engine : has a

    class Engine{
        +String model
    }
    class Car{
        -Engine engine
    }
```
