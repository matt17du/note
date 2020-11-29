### 1.三范式

降低了数据的冗余

查询效率更高



### 2三种日志

binlog

redolog

undolog



#### binlog和redolog区别

- binlog是server层，redolog是innodb存储引擎特有的；
- binlog是逻辑层面的，记录的是更新了表中的那条数据，redolog记录的是对数据页的修改；
- binlog文件是追加的，redolog文件是循环写的，有俩个指针write pos:当前写的位置， check point：察除的位置

![image-20201111221802647](img/image-20201111221802647.png)



幻读：一个事务前后俩次查询同一范围内的数据，看到的数据行数不同。





- select ... lock in share mode（共享锁，S锁）
- select ... for update （排它锁，X锁）

### 3.锁

如果未使用索引则使用表锁



### 表的设计

#### 主表和从表

添加外键的表是从表，指向的表是主表。

#### left join和join区别

left join匹配左表的所有记录，以及右表中和左表匹配的记录

join:inner join 缩写，左表和右表匹配的记录。