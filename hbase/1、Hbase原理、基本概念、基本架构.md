[Hbase原理、基本概念、基本架构](http://blog.csdn.net/woshiwanxin102213/article/details/17584043)

[Apache HBase™ 参考指南](http://abloz.com/hbase/book.html)

HBase是一个构建在HDFS上的分布式列存储系统；
HBase是基于Google BigTable模型开发的，典型的key/value系统；
HBase是Apache Hadoop生态系统中的重要一员，主要用于海量结构化数据存储；

### Hbase表的特点
```
1、大：一个表可以有数十亿行，上百万列；
2、无模式：每行都有一个可排序的主键和任意多的列，列可以根据需要动态的增加，同一张表中不同的行可以有截然不同的列；
3、面向列：面向列（族）的存储和权限控制，列（族）独立检索；
4、稀疏：空（null）列并不占用存储空间，表可以设计的非常稀疏；
5、数据多版本：每个单元中的数据可以有多个版本，默认情况下版本号自动分配，是单元格插入时的时间戳；
6、数据类型单一：Hbase中的数据都是字符串，没有类型。
```


### 数据模型
Hbase的逻辑视图，见[以上链接](http://blog.csdn.net/woshiwanxin102213/article/details/17584043)

### hbase基本概念
```
RowKey：是Byte array，是表中每条记录的“主键”，方便快速查找，Rowkey的设计非常重要。
Column Family：列族，拥有一个名称(string)，包含一个或者多个相关列
Column：属于某一个columnfamily，familyName:columnName，每条记录可动态添加
Version Number：类型为Long，默认值是系统时间戳，可由用户自定义
Value(Cell)：Byte array
```

### Hbase物理模型
每个column family存储在HDFS上的一个单独文件中，空值不会被保存。
Key 和 Version number在每个 column family中均有一份；
HBase 为每个值维护了多级索引，即：<key, column family, column name, timestamp>

```
1、Table中所有行都按照row key的字典序排列；
2、Table在行的方向上分割为多个Region；
3、Region按大小分割的，每个表开始只有一个region，随着数据增多，region不断增大，当增大到一个阀值的时候，region就会等分会两个新的region，之后会有越来越多的region；
4、Region是Hbase中分布式存储和负载均衡的最小单元，不同Region分布到不同RegionServer上。
```

### Hbase基本组件说明
