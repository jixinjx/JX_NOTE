
Greenplum([[OLAP和OLTP#OLAP On-Line Analytical Processing|OLAP]])
Greenplum的技术架构也是MPP[[数据库类型]]，对内存资源要求不是很高，但是对传输的带宽要求比较高。
Greenplum的一个很重要的特点是真的可以平行扩展。impala 实际在计算的时候还是需要Slave节点去做各个其他节点的一些聚合计算的。但是GreenPlum可以通过高速网络把DataNode上的数据不断分发分片到其他DataNode节点进行归并计算，让计算单点做到最低。