分布键设置是否合理会用倾斜率进行测试

再GP可以通过 /d+表名查看表情况

空间回收
VACUUM 进行空间回收

关联的时候，优先关联小表

表关联的时候，最好不要用有表达式的作为条件进行关联，可以先创建临时表处理，然后再进行Join


IDL
ICL
IML 标准化
IOL
ITL


避免对大表 update操作，尽量采用DELETE+INSERT方式实现

union操作可以union all+group by去重