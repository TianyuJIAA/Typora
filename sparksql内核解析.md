# 第二章 spark基础知识介绍

## 理解RDD

### RDD的概念

定义：RDD是spark的核心数据结构，全称是弹性分布式数据集，本质是一种分布式的内存抽象，表示一个只读的数据分区集合(Partition)

5大特性：

|       特性名        | 特性类型 |            特性定义             |
| :-----------------: | :------: | :-----------------------------: |
|    dependencies     |   变量   |         刻画了RDD的依赖         |
|       compute       |   方法   |    刻画了生成该RDD的计算规则    |
|     partitions      |   变量   | 刻画了集群中该RDD所有的数据分片 |
|     partitioner     |   方法   |     切分数据集的规则或方法      |
| preferred locations |   变量   |   刻画了数据分片物理位置偏好    |

### RDD核心抽象

<img src="typora_imagine/image-20230617130228059.png" alt="image-20230617130228059" style="zoom:50%;" />

# 第三章 Spark Sql执行全过程概述

## 从SQL到RDD：一个简单的案例

- 本节主要是通过一段简单的sql来概述spark的执行过程

### 结构化API执行概述

- 整个过程是：将编写的代码以spark作业的形式进行提交，然后代码交由Catalyst优化器决定执行逻辑，并制定执行计划，最后代码运行并将结果返回给用户

  <img src="typora_imagine/image-20230622181929096.png" alt="image-20230622181929096" style="zoom:50%;" />

### 执行过程概述

- sql执行全过程概述

  - Unresolved LogicalPlan:未解析的逻辑算子树，这里只是数据结构，不包含数据信息(表的来源等。。)
  - Analyzed LogicalPlan: 解析后的逻辑算子树，节点中绑定各种数据信息
  - Optimized LogicalPlan: 优化后的逻辑算子树，使用优化规则对低效的逻辑计划进行转换
  - 在逻辑计划后的物理计划可能有多个，最终需要通过代价模型(策略)选择最优的物理计划
  - 在Prepared SparkPlan这里

  <img src="typora_imagine/image-20230622192807509.png" alt="image-20230622192807509" style="zoom:50%;" />

- 实际转换过程

### 测试代码查看执行过程



