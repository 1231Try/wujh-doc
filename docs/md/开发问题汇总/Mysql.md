MySQL函数

```
一、NVL(exp1,exp2)

--如果第一个参数的值不为空，则返回第一个参数的值;否则，返回第二个参数的值。

SQL> select NVL(1000,12) FROM DUAL;

NVL(1000,12)

1000

SQL> select NVL(null,12) FROM DUAL;

NVL(NULL,12)

12

二、NVL2(exp1,exp2,exp3)

--如果第一个参数的值非空，返回第二个参数的值;否则，返回第三个参数的值。

SQL> SELECT NVL2(12,1,-1) FROM dual;

NVL2(12,1,-1)

1
```

