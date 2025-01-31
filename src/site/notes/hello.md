---
{"dg-publish":true,"permalink":"/hello/","created":"2025-01-31T22:24:55.224+02:00","updated":"2025-01-31T22:58:27.375+02:00"}
---

# hello
---

![Truth Table.png](/img/user/assets/img/Truth%20Table.png)

```mermaid
classDiagram
    Teacher -- Student

    class Student{
        +Teacher myTeacher
    }
    class Teacher{
        +students: Student[]
    }
```
