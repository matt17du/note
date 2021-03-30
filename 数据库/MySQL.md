## 使用

### 卸载

1、停止MySQL服务

2、卸载MySQL相关的程序

从控制面板进入卸载mysql相关的应用程序



3.删除mysql文件夹

本人安装目录在C盘，首先打开C:\Program Files，删除MySQL安装文件夹和数据文件夹

打开隐藏文件ProgramData文件夹，删除下面的MySQL文件

4.删除注册表

step1：Windows+R-->regedit-->打开注册表

tep2：根据路径打开并删除：

 HKEY_LOCAL_MACHINE/SYSTEM/ControlSet001/Services/Eventlog/Applications/MySQL 
HKEY_LOCAL_MACHINE/SYSTEM/ControlSet002/Services/Eventlog/Applications/MySQL 
HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services/Eventlog/Applications/MySQL
HKEY_LOCAL_MACHINE/SYSTEM/CurrentControlSet/Services一般服务会以相同的名字(名字通常是MySQL)



还有就是F3或Ctrl+F打开查找框，输入MySQL，注意焦点放在计算机上

还有重要的一步删除Connector Net XXX注册表，大家失败的原因好多也是在这个注册表上面

查出的MySQL注册表直接删掉



### 安装

参考该[博客](https://blog.csdn.net/baidu_36602427/article/details/88387630?utm_medium=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control&depth_1-utm_source=distribute.pc_relevant_t0.none-task-blog-BlogCommendFromMachineLearnPai2-1.control)

[官网](https://downloads.mysql.com/archives/community/)

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210118221521.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210118221607.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210118221328.png)



#### 1.解压安装

1.将下载完的 zip 包解压到相应的目录，这里我将解压后的文件夹放在 D:\IDE\mysql-5.7.25 下。解压后的文件如图所示：



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210118221718.png)



2.在该文件夹下创建 my.ini 配置文件，编辑 my.ini 配置以下基本信息：



```
[mysql]
# 设置mysql客户端默认字符集
default-character-set=utf8
 
[mysqld]
# 设置3306端口
port = 3306

# 设置mysql的安装目录
basedir=D:\\IDE\\mysql-5.7.25

# 设置 mysql数据库的数据的存放目录（MySQL8.0+ 不需要以下配置，系统自己生成即可，否则有可能报错）
datadir=D:\\WorkPlace\\SqlData

# 允许最大连接数
max_connections=20

# 服务端使用的字符集默认为8比特编码的latin1字符集
character-set-server=utf8

# 创建新表时将使用的默认存储引擎
default-storage-engine=INNODB

sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES
```

3、以管理员身份打开 cmd 命令行工具，进入目录：

```
D:
cd D:\develop\env\mysql-5.7.25-winx64
```

#### 2.注册服务

1.运行`mysqld --initialize --console`初始化数据库，如果提示缺少某个 .dll 文件，自行百度下载，然后将下载好的 .dll 文件放入 C:\Windows\System32（32位） 或 C:\Windows\SysWOW64 （64位）目录下即可，最好是两个目录下都放一份。如果提示 mysqld.exe 应用程序无法正常启动，则安装DirectX修复软件进行修复。
初始化完成后，会输出 root 用户的初始默认密码，如下图所示，!0A6yhdq>lcY 就是初始密码，最好记下来，后续登录需要用到，你也可以在登录后修改密码

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210118222432.png)



2.运行`mysqld install`，若提示 “Service successfully installed.” 表示安装成功。



#### 3.修改密码

1、执行`net start mysql`启动MySQL



2.运行`mysql -u root -p`后根据提示输入初始密码，回车后即可登录进MySQL



3、修改密码命令的格式为：`set password for userName@localhost = password('newPassword');`

注意不要盲目复制，修改成自己的用户名和新密码，刚初安装完默认的用户名是root，由于我的数据库仅作为学习使用，里面没有什么绝密的军事资料，就设一个简单易记的密码：root



4.输入`exit`后回车，再运行`mysql -u root -p`后就可以用新密码登录了。

#### 4.添加环境变量

1、右键此电脑 >> 高级系统设置 >> 环境变量 ，新建系统变量 MYSQL_HOME，变量值是安装MySQL的根目录：D:\develop\env\mysql-5.7.25-winx64



2、编辑系统变量 Path >> 新建 >> 将 %MYSQL_HOME%\bin 添加到尾行 >> 确定。

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





limit



```mysql
SELECT * 
FROM student
LIMIT 0, 2   # 0：表示索引 2:表示几条数据而不是右边界， 从0开始


#
LIMIT n # 表示0开始到n-1不包括n
```

日期函数

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210310105753.png)





count(1)

count(*)





## 面试





**hash索引：**根据索引计算哈希值， 不支持排序不支持范围查询





mysql默认隔离级别：可重复读