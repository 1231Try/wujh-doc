Hbase

定义：大数据解决方案中的数据库，分布式的具有时间版本的面向列的非关系型数据据，基于hdfs之上做的存储

解决问题：解决海量数据实时查询

问题：运维，测试成本较高

1、Hbase连接

```bash
hbase shell
```

2、查看Hbase表信息

```bash
list
```

3、查看某一个表的数据

```bash
scan 'obds:OR_WAIT_CF_202309'
```

