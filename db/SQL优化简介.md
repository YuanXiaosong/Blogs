# SQL优化简介

## 基础概念
### 基础概念-SQL分类
#### SQL语句可以分成4类
##### - 数据查询语句
```
select
```

##### - DML数据操作语句
```
insert
update
delete
```

##### - DDL数据定义语句
```
create
drop
alter
modify
```

##### - 事务控制语句    
```
select
```


### 基础概念-名词解释
##### - cardinality基数
可理解为结果集的记录数（rows）。

##### - Selectivity可选择性
满足筛选条件的记录数/筛选前的总行数，越小越好。

##### - 直方图
统计列数据的分布情况，适用于分布不均匀的数据。

##### - 回表
通过index的rowid返回结果集，逐条查询；
如果结果集较大，数据分布又比较分散，会造成严重IO问题。

##### - clustering factor集群因子
数据在数据块里是否根据索引键值集中分布；
大小在数据行数和所占有数据块数量之间。

##### - 统计信息
可通过dbms_stats包和analyze来收集；
包括表的信息，索引的信息，列的信息等。


### 基础概念-索引分类
##### - B树索引
- 索引键值和rowid数据存在叶子节点，所有叶子节点都在同一层，有序排列，并且是左右互联的；
- 根节点下有分支块，分支块也可以分层，最终指向叶子节点；
- 索引扫描从根节点到分支节点到叶子节点只需要几次就可找到具体数据的rowid，查询数据的时间基本稳定和可控。

##### - 位图索引
- 叶子节点包含被索引键值，对应rowid下限、上限、位图段；
- 不适合OLTP系统，索引维护修改成本高；
- 节约空间，能快速处理and或者or条件。


### 基础概念-数据访问路径
- 全表扫描（按数据块读取，多块读，数据来增加和高水位线会造成性能问题）
- Rowid（dbms_rowid包，能找到数据所在的数据文件、数据块所在数据块行数信息）
- 索引唯一扫描（扫描索引一次，返回一条数据，一次数据块读取）
- 索引范围扫描（比相应的唯一扫描多一次逻辑读，从叶子节点从左到右一直读取到相邻的终点）
- 索引全扫描（通过根节点找到最左边的叶子节点，然后用叶子节点相互连接的指针，扫描其他叶子节点，可以达到排序效果）
- 索引快速全扫描（类似于索引全扫描，区别在：只适用于CBO，可使用多块读，可并行，结果不一定有序，根据数据物理存储顺序扫描）
- 索引跳跃式扫描（skip，对于复合索引的非前导列使用索引查询）


### 基础概念-表连接方式和连接类型
##### 表连接方式
- **循环嵌套**
小表驱动大表（结果集），优点是快速响应，能够更快的返回部分结果。

- **排序合并**
先排序，然后合并连接，可用非费等值连接。

- **Hash连接**
先分别将两张表连接字段按照相同的hash算法放到bucket里，然后再进行连接，通常用于等值连接，只适用于CBO。

- **笛卡尔连接**
无连接条件，交叉连接。

##### 连接类型（SQL的写法直接决定连接类型）
- **内连接**
连接结果只包含完美满足连接条件的记录

- **外连接**
outer join: left, right, full

- **半连接**
找到第一条满足条件的即可，会对连接条件去重

- **反连接**
not in, not exists, <>all()转换成反连接


## 优化器
### 优化器-RBO基于规则（rule）
- RBO Path1: Single Row by Rowid（等级最高）
- RBO Path2: Single Row by Cluster Join
- RBO Path3: Single Row by Hash Cluster Key with Unique or Primary Key
- RBO Path4: Single Row by Unique or Primary Key
- RBO Path5: Clustered Join
- RBO Path6: Hash Cluster Key
- RBO Path7: Indexed Cluster Key
- RBO Path8: Composite Index
- RBO Path9: Single-Column Indexes
- RBO Path10: Bounded Range Search on Indexed Columns
- RBO Path11: Unbounded Range Search on Indexed Columns
- RBO Path12: Sort Merge Join
- RBO Path13: MAX or MIN of Indexed Column
- RBO Path14: ORDER BY on Indexed Column
- RBO Path15: Full Table Scan（等级最低）

上面的执行路径中，RBO认为越往下执行代价越大，即等级越低。在RBO生成执行计划时，如果它发现有等级高的执行路径可用，则肯定会使用等级高的路径，而不管任何其他影响性能的元素，即RBO通过上面路径的等级决定执行路径的代价，执行路径的等级越高，则使用该执行路径的代价越小。

### 优化器-CBO
在使用CBO时，需要有表和索引的统计数据（分析数据）作为基础数据，有了这些数据，CBO才能为各个执行计划计算出相对准确的代价，从而使CBO选择最佳的执行计划。
一个查询耗费的资源可以被分成3个基本组成部分：I/O代价、CPU代价、network代价。
- I/O代价是将数据从磁盘读入内存所需的代价。访问数据包括将数据文件中数据块的内容读入到SGA的数据高速缓存中，在一般情况下，该代价是处理一个查询所需要的最主要代价，所以我们在优化时，一个基本原则就是降低查询所产生的I/O总次数。
- CPU代价是处理在内存中数据所需要的代价，如一旦数据被读入内存，则我们在识别出我们需要的数据后，在这些数据上执行排序（sort）或连接（join）操作，这需要耗费CPU资源。
- 对于需要访问跨节点（即通常说的服务器）数据库上数据的查询来说，存在network代价，用来量化传输操作耗费的资源。查询远程表的查询或执行分布式连接的查询会在network代价方面花费比较大。

### 优化器-模式
##### 优化器模式Choose/first rows/all rows/rule
- CHOOSE是根据实际情况，如果数据字典中包含被引用的表的统计数据，即引用的对象已经被分析，则就使用CBO优化器，否则为RBO优化器。
- ALL_ROWS为CBO优化器使用的第一种具体的优化方法，是以数据的吞吐量为主要目标，以便可以使用最少的资源完成语句。
- FIRST_ROWS为优化器使用的第二种具体的优化方法，是以数据的响应时间为主要目标，以便快速查询出开始的几行数据。
- FIRST_ROWS_[1|10|100|1000]为优化器使用的第三种具体的优化方法，让优化器选择一个能够把响应时间减到最小的查询执行计划，以迅速产生查询结果的前n行。该参数为Oracle 9I新引入的。
- RULE是制定使用RBO优化器。


## 执行计划
### 执行计划-获取方式
##### 获取执行计划的常用方式
1. PL/SQL sql windows下，快捷键F5；
2. SQLplus > set autotrace on/traceonly;
3. Explaine plan for sql语句；
查看oracle系统根据统计信息给出的执行计划
```
select * from table(dbms.xplan.display)
```
查看真实的sql执行计划
```
select * from table(dbms_xplan.display_cursor(sql_id, child_number));
select t.SQL_ID, t.CHILD_NUMBER, t.PARSING_SCHEMA_NAME, t.* from V$sql t where t.SQL_TEXT like '%emp%' and t.PARSING_SCHEMA_NAME = 'C##SID';
```
4. 10046事件；

### 执行计划解读

## 常用hint
### 常用hint
##### 指示优化器的方法与目标
- ALL_ROWS 基于代价的优化器，以吞吐量为目标
```
/*+ ALL_ROWS */
```

- FIRST_ROWS(n) 基于代价的优化器，以响应时间为目标
```
/*+ FIRST_ROWS(n) */
```

- CHOOSE 根据是否有统计信息，选择不同的优化器
```
/*+ CHOOSE */
```

- RULE 使用基于规则的优化器
```
/*+ RULE */
```

##### 指示连接类型
- USE_NL 使用嵌套连接
```
/*+ USE_NL (table [,table, ...]) */
```

- USE_MERGE 使用排序，合并连接
```
/*+ USE_MERGE (table [,table, ...]) */
```

- USE_HASH 使用HASH连接
```
/*+ USE_HASH (table [,table, ...]) */
```

注意：*如果表有 alias（别名），则上面的 table 指的是表的别名，而不是真实的表名*


##### 指示存储路径的hints
- FULL 指定该表使用全表扫描
```
/*+ FULL (table) */
```

- ROWID 指定对该表使用rowid存取方法，该提示用的较少
```
/*+ ROWID (table) */
```

- INDEX 使用该表上指定的索引对表进行索引扫描
```
/*+ INDEX (table [index]) */
```

- INDEX_FFS 使用快速全表扫描
```
/*+ INDEX_FFS (table [index]) */
```

- NO_INDEX 不使用该表上指定的索引进行存取，仍然可以使用其它的索引进行索引扫描
```
/*+ NO_INDEX (table [index]) */
```



## SQL开发规范和优化建议
### SQL开发规范
1. SQL语句统一采用大写；
2. 相同含义的SQL保持完全一致；
相同业务含义的SQL，尽量保持大小写一致、空格一致等书写完全一致，减少重复解析
3. 使用绑定变量；
4. 禁用隐式转换；
a）转换发生在索引列上，影响执行计划，导致本该走索引的却不走索引
b）转换发生在普通非索引列上，造成多余的转换开销
Oracle隐式转换的规则如下：
（1）比较时，一般是字符型转换为数值型，字符型转换为日期型
（2）算式运算时，一般把字符型转换为数值型，字符型转换为日期型
（3）连接时 `||`，一般是把数值型转换为字符型，日期型转换为字符型
（4）赋值、调用函数时，以定义的变量类型为准
5. 禁止在SQL查询中使用 `*`，按需取字段；
6. OLTP类型的应用，单条SQL单次查询返回结果集限制在1万条以内；
如果没有对查询结果集进行限制，很有可能因查询结果集过大，造成应用服务器处理进程占用内存过高，最终将JVM内存耗尽，并进而造成应用服务器宕机，从而影响业务开展，造成严重后果
7. 大表关联时，非同表条件不能使用 `OR` 关联筛选；
8. 不允许使用 `OR IS NULL` 方式拼接SQL；
对于这种情况的需求，就需要考虑在应用层将该SQL拆成多个SQL来执行，而不允许使用 `OR IS NULL` 的方式拼接SQL



### 常用优化建议
- 能写在内层的过滤条件不要写在外层
- 尽量避免笛卡尔积的连接方式
- 注意排序的使用
带有 `DISTINCT`，`UNION`，`MINUS`，`INTERSECT`，`ORDER BY` 的SQL语句会启动SQL引擎执行耗费资源的排序（sort）功能。`DISTINCT`需要一次排序操作，而其它至少需要执行两次排序。