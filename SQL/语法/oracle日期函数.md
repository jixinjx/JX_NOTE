## 求两个日期的事件差

```sql
select 
round(to_number(TO_DATE('2012-02-20 17:45:04','yyyy-mm-dd hh24:mi:ss')-TO_DATE('2012-02-19 08:34:04','yyyy-mm-dd hh24:mi:ss'))*1440) as Minite   
from dual; 
```

两个Date类型字段：START_DATE，END_DATE，计算这两个日期的时间差（分别以天，小时，分钟，秒，毫秒）：

天：

ROUND(TO_NUMBER(END_DATE - START_DATE))

小时：

ROUND(TO_NUMBER(END_DATE - START_DATE) * 24)

分钟：

ROUND(TO_NUMBER(END_DATE - START_DATE) * 24 * 60)

秒：

ROUND(TO_NUMBER(END_DATE - START_DATE) * 24 * 60 * 60)

毫秒：

ROUND(TO_NUMBER(END_DATE - START_DATE) * 24 * 60 * 60 * 1000)
