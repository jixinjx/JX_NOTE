Impala

impala 是 一种常用的OLAP [[OLAP和OLTP#OLAP On-Line Analytical Processing]]数据分析引擎。

由于很多计算数据都在内存中运行，大内存下性能相对比较高，但是对内存要求比较高。

生态兼容性比较好支持kudu, hdfs, hbase等多种数据库，支持parque等列存压缩格式。

impala比其他MPP的先进之处在于数据流量和计算还是很少经过master的，执行任务的分析和创建是随机分布在slave 节点的query planner, 再根据 上的信息去数据实际对应的节点的query coordinator上执行查询数据的行为，最终由入口Slave聚合数据返回Client。

impala的适用场景是数据量在亿到十亿级别，对时间延迟在亚秒级，能够支持join查询和其他即席查询的场景。