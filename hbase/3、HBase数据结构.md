HBase相关术语
```
基于列: column-oriented
行: row
列组: column families
列: column
单元: cell
```

不同与一般关系型数据库的两点
```
1、适合于非结构化数据存储的数据库
2、HBase是基于列的而不是基于行的模式
```



Google's BigTable论文 清楚地解释了什么是BigTable：
Bigtable是一个疏松的分布式的持久的多维排序的map,这个map被行键,列键,和时间戳索引.每一个值都是连续的byte数组.(A Bigtable is a sparse, distributed, persistent multidimensional sorted map. The map is indexed by a row key, column key, and a timestamp; each value in the map is an uninterpreted array of bytes.)

HBase 和BigTable都是在分布式文件系统上构建的,所以基础的文件存储能够散布在分布式文件系统的机器上.


