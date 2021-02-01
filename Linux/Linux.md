### 安装centos





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223165457.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223165531.png)







![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223165627.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223165756.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223165833.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223165858.png)







![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223165922.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223165944.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223170017.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223170051.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223170129.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223170218.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223170315.png)



开机回车



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223170546.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223170716.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223170902.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223171000.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223171104.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223171209.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223171317.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223171702.png)



200mb    9536mb    2048mb

标准分区，/boot，要大于200mb,文件系统， ext4

根分区新建，设备类型“标准分区”，挂载点为“/”，文件系统为“ext4”

swap分区设置，文件系统为“swap”

**文件系统要选择对**



不启用Kdump



修改主机名



开始安装，设置Root密码即可等待安装完成





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223172257.png)



重启同意许可证完成配置即可





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223172950.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223173023.png)





完成配置在线账号跳过、设置账号注销使用root登录即可



### 常用的命令

帮助命令

```
man cd
cd --help
```

文件目录命令

```
touch hello.txt
vim hello.txt
mkdir aa

// 文件全部显示出来
cat hello.txt
// 一页
more hello.txt
less hello.txt

// 显示更多的信息
ls -l
//隐藏的文件也会显示出来
ls -a 
ls 

cp hello.txt copy.txt
mv hello.txt a.txt
mv hello.txt ../

// 删除文件
rm -rvf a.txt 

cd /mnt
pwd



// 统计字数
wc a.txt

chmod 777 hello.txt
```

ipcs -m

ipcrm -m [shmid]



top命令:系统资源使用状况

```
top - 　　　　系统当前时间
up 　　　　　 系统已开机多长时间
user 　　　　 当前用户数
load average cpu平均负载，三个数值分别为，1分钟，5分钟，15分钟
Tasks 　　 系统当前进程数，total：总进程数，running：正在运行的进程数，sleeping：睡眠的进程数，stopped：停止的进程数，zombie：僵尸进程数
%Cpu(s) cpu使用率，us：用户使用cpu百分百，sy：系统内核使用cpu百分百，id：剩余的cpu百分百
Mem 　　　 内存使用信息，total：总内存大小，free：空闲的内存，used：已使用的内存，buff/cache：缓存的内存大小
Swap 　　 虚拟内存信息
PID　　　　 进程id
USER　　　　 进程所有者
PR　　　　　　 优先级
NI　　　　　　　nice值，负值表示高优先级，正值表示低优先级
VIRT 　　　　　 进程使用的虚拟内存总量
RES 　　　　　 进程使用的物理内存大小
SHR 　　　　　 共享内存大小
S 　　　　　　 进程状态，D：不可中断的睡眠状态，R：运行，S：睡眠，T：跟踪/停止，Z：僵尸进程
%CPU 　　　　 进程使用的CPU占用百分比
%MEM 　　　　 进程使用的物理内存百分比
TIME+ 　　　　 进程使用的CPU时间总计
COMMAND　　 命令名
```



```shell
kill -9 9000
// 查看进程
ps -ef
// 查看网络情况
netstat -anp 
netstat -anp | grep 9000   // 查看端口号为9000的进程
```





ps -ef





UID    PID    PPID    C   STIME   TTY    TIME     CMD

zzw   14124  13991   0   00:38   pts/0   00:00:00  grep --

 

**UID   ：程序被该 UID 所拥有**

**PID   ：就是这个程序的 ID** 

**PPID  ：则是其上级父程序的ID**

**C     ：CPU使用的资源百分比**

**STIME ：系统启动时间**

**TTY   ：登入者的终端机位置**

**TIME  ：使用掉的CPU时间。**

**CMD  ：所下达的是什么指令**

#### 关机

```java
shutdown -h now // 立即关机
```

重启

```java
shutdown -r now // 立即重启
```





### 网络





#### 设置NAT

##### 1.设置主机虚拟网络v8

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210131174231.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210131174307.png)



设置静态ip

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210131174355.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210131174517.png)



##### 2.设置虚拟机网络



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210131174612.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210131174702.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210131174736.png)



子网ip，主机和虚拟机 需要在同一网段（因为在一个内网下）

**关闭windows防火墙**



##### 3.设置centos网络



```java
vim /etc/sysconfig/network-scripts/ifcfg-ens33
```



```java
TYPE="Ethernet"
PROXY_METHOD="none"
BROWSER_ONLY="no"
BOOTPROTO="dhcp"
DEFROUTE="yes"
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens33"
UUID="6b84fa31-a207-4928-9e53-61ad2ec7b485"
DEVICE="ens33"
ONBOOT="yes"
```

```java
TYPE="Ethernet"
PROXY_METHOD="none"
BROWSER_ONLY="no"
BOOTPROTO="static" // 更改该值
DEFROUTE="yes" 
IPV4_FAILURE_FATAL="no"
IPV6INIT="yes"
IPV6_AUTOCONF="yes"
IPV6_DEFROUTE="yes"
IPV6_FAILURE_FATAL="no"
IPV6_ADDR_GEN_MODE="stable-privacy"
NAME="ens33"
UUID="6b84fa31-a207-4928-9e53-61ad2ec7b485"
DEVICE="ens33"
ONBOOT="yes"   //
IPADDR=192.168.96.129   // ip 地址,前三位和子网ip一致
NETMASK=255.255.255.0   //
GATEWAY=192.168.96.2    // ip.2
DNS1=114.114.114.114    // 默认
```

重启网络

```java
service network restart
```

```
systemctl restart network
```

如果无法上网点击有线连接即可

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223174649.png)



### 虚拟机克隆

记得一定要关机下



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223174740.png)







![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223174902.png)







![](https://raw.githubusercontent.com/matt17du/img/main/img/20201223175010.png)



### 安装ssh

检查是否安装ssh



```java
yum list installed | grep openssh-server
```

安装ssh

```java
yum install -y openssl openssh-server
```

配置

```java
vim /etc/ssh/sshd_config
```

以下打开

**port,ListenAddress**

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201218140734.png)



**PermitRootLogin,PubkeyAuthentication,Password**



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201218140817.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201218140845.png)



#### 退出

```c
logout 123.56.135.43 //退出ssh连接
```



### 安装gcc gcc++

```java
yum -y install gcc gcc-c++ kernel-devel //安装gcc、c++编译器以及内核文件
```

```
gcc --version

g++ --version
```



### 使用SSH

```java
systemctl start sshd.service
systemctl enable sshd.service
```





```java
ssh root@123.56.135.43
    //用户名@ip
```

退出

```JAVA
Logout
exit
```





### JDK

[jdk](https://www.oracle.com/java/technologies/javase/javase-jdk8-downloads.html)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231172604.png)



下载解压到/opt目录下，之后 vim /etc/profile,添加如下内容



```java
JAVA_HOME=/opt/jdk1.8
PATH=$PATH:$JAVA_HOME/bin
CLASSPATH=$JAVA_HOME/lib
export JAVA_HOME PATH CLASSPATH
```

配置文件生效

```java
临时生效：source /etc/profile
永久生效：reboot
```

### tomcat

[tomcat8.5](https://tomcat.apache.org/download-80.cgi)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231172634.png)

下载安装解压即可



#### 启动

```java
./startup.sh
```



### MySQL

```java
yum install mysql*
    
yum install mariadb-server
```

```java
systemctl start mariadb.service
```

指定密码

```java
mysqladmin -u root password root
```

#### 开启远程连接的权限


```java
update user set host='%' where user = 'root'; 

flush privileges;
```

```java
grant all privileges on *.* to root@'%'  identified by 'root'; 
```





### 防火墙

查看防火墙状态

```java
systemctl status firewalld.service
```

关闭防火墙

```java
systemctl stop firewalld.service
```

禁止开机启动

```java
systemctl disable firewalld.service
```

### nginx-openresty

openresty:对nginx进行了封装，首先在下面链接下载



[openresty](http://openresty.org/cn/download.html)

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201218180025.png)



之后发送到linux中，解压即可

```java
tar -zxvf xx.tar.gz
```

前提



```java
yum -y install gcc gcc-c++ kernel-devel //安装gcc、c++编译器以及内核文件
```



```java
yum install pcre-devel openssl-devel gcc curl
```

切换到解压目录

```java
cd openresty-VERSION/
```

编译

```java
make
```

安装

```java
sudo make install
```

#### 启动

```java
sbin/nginx -c conf/nginx.conf
```

#### 重启

```java
sbin/nginx -s reload
```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201218155237.png)



## redis



**错误**

**server.c:5171:176: 错误：‘struct redisServer’没有名为‘maxmemory’的成员**



1、安装gcc套装：

yum install cpp
yum install binutils
yum install glibc
yum install glibc-kernheaders
yum install glibc-common
yum install glibc-devel
yum install gcc
yum install make
2、升级gcc

yum -y install centos-release-scl

yum -y install devtoolset-9-gcc devtoolset-9-gcc-c++ devtoolset-9-binutils

scl enable devtoolset-9 bash

3、设置永久升级：

echo "source /opt/rh/devtoolset-9/enable" >>/etc/profile

4、安装redis：





[redis](https://redis.io/)



```java
chmod 777 xxxx
// 进入redis安装目录
// 编译
make
// 安装
make install
```

```java
make clean
```





## top

用于查看系统资源使用状况和进程的基本信息

```java
top -H
```

在终端中输入`top`，回车后会显示如下内容：



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201219083353.png)



### 一、系统信息统计

前五行是系统整体状态的统计信息展示区域。下面分别介绍每一行中的内容：

#### 1、第一行显示服务器概况

如下所示，第一行列出了服务器运行了多长时间，当前有多少个用户登录，服务器的负荷情况等，使用`uptime`命令能获得同样的结果。

```
top - 21:48:39 up  8:57,  2 users,  load average: 0.36, 0.24, 0.14
       /         /        /                \
   当前时间  运行时长   当前登录用户数  平均负载（1分钟、5分钟、15分钟）
```

平均负载的值越小代表系统压力越小，越大则代表系统压力越大。通常，我们会以最后一个数值，也就是15分钟内的平均负载作为参考来评估系统的负载情况。

对于只有单核cpu的系统，`1.0`是该系统所能承受负荷的边界值，大于1.0则有处理需要等待。

一个单核cpu的系统，平均负载的合适值是`0.7`以下。如果负载长期徘徊在1.0，则需要考虑马上处理了。超过1.0的负载，可能会带来非常严重的后果。

当然，多核cpu的系统是在前述值的基础上乘以cpu内核的个数。如对于多核cpu的系统，有N个核则所能承受的边界值为`N.0`。

可以使用如下命令来查看每个处理器的信息：

```
cat /proc/cpuinfo
```

如果只想计算有多少个cpu内核，可以使用如下命令：

```
cat /proc/cpuinfo | grep 'model name' | wc -l
```

#### 2、第二行是进程信息：

```
Tasks: 322 total,   2 running, 320 sleeping,   0 stopped,   0 zombie
        /                /            /             /            /
    进程总数      正运行进程数    睡眠进程数   停止进程数    僵尸进程数
```

#### 3、第三行是CPU信息：

```
%Cpu(s):  
5.0 us      用户空间CPU占比
1.7 sy      内核空间CPU占比
0.0 ni      用户进程空间改过优先级的进程CPU占比
93.0 id     空闲CPU占比
0.0 wa      待输入输出CPU占比
0.3 hi      硬中断（Hardware IRQ）CPU占比
0.0 si      软中断（Software Interrupts）CPU占比
0.0 st      - 
```

##### **us,sy**



#### 4、第四行是内存信息：

```
KiB Mem:   1010504 total,   937416 used,    73088 free,    23708 buffers
                /                /                /                /
            物理内存总量      使用中总量        空闲总量        缓存的内存量
```

#### 5、第五行是swap交换分区信息：

```
KiB Swap:  1046524 total,   280708 used,   765816 free,   365556 cached Mem
                /                /                /                /
            交换区总量      使用中总量        空闲总量        缓存的内存量
```

使用中的内存总量（used）指的是现在系统内核控制的内存数，空闲内存总量（free）是内核还未纳入其管控范围的数量。纳入内核管理的内存不见得都在使用中，还包括过去使用过的现在可以被重复利用的内存，内核并不把这些可被重新使用的内存交还到free中去，因此在[linux](http://lib.csdn.net/base/linux)上free内存会越来越少，但不用为此担心。

如果出于习惯去计算可用内存数，这里有个近似的计算公式：第四行的free + 第四行的buffers + 第五行的cached，按这个公式此台服务器的可用内存：73088+23708+365556 = 451M。

对于内存监控，在top里我们要时刻监控第五行swap交换分区的used，如果这个数值在不断的变化，说明内核在不断进行内存和swap的数据交换，这是真正的内存不够用了。

### 二、进程（任务）状态监控

第七行及以下显示了各进程（任务）的状态监控。各列所代表的含义如下：

```
PID         进程id
USER        进程所有者
PR          进程优先级
NI          nice值。负值表示高优先级，正值表示低优先级
VIRT        进程使用的虚拟内存总量，单位kb。VIRT=SWAP+RES
RES         进程使用的、未被换出的物理内存大小，单位kb。RES=CODE+DATA
SHR         共享内存大小，单位kb
S           进程状态。D=不可中断的睡眠状态 R=运行 S=睡眠 T=跟踪/停止 Z=僵尸进程
%CPU        上次更新到现在的CPU时间占用百分比
%MEM        进程使用的物理内存百分比
TIME+       进程使用的CPU时间总计，单位1/100秒
COMMAND     进程名称（命令名/命令行）
```

Cpu(s)表示的是 所有用户进程占用整个cpu的平均值，由于每个核心占用的百分比不同，所以按平均值来算比较有参考意义。
%CPU显示的是进程占用一个核的百分比，而不是整个cpu（12核）的百分比，有时候可能大于100，那是因为该进程启用了多线程占用了多个核心，所以有时候我们看该值得时候会超过100%，但不会超过总核数*100。

### 三、与top交互

- 按键`b`打开或关闭 运行中进程的高亮效果
- 按键`x`打开或关闭 排序列的高亮效果
- `shift + >` 或 `shift + <` 可以向右或左改变排序列
- `f`键，可以进入编辑要显示字段的视图，有 * 号的字段会显示，无 * 号不显示，可根据页面提示选择或取消字段。



## 用户与文件权限

添加组

```java
groupadd g1
```

删除组

```java
groupdel g1
```

添加用户

```java
useradd -g g1 u1
```
设置密码
```java
passwd u1 // 设置密码
```

删除u1

```java
userdel -r u1
```

u1是否存在

```java
id u1
```

当前是哪个用户

```java
who am i
```
切换用户

```java
su - u1
```

以管理员运行

```java
sudo ls
```







## cygwin

### 无法使用vim

E437: terminal capability "cm" required 错误；

```java
export TERM=xterm    
```

### **挂载**

/cygdrive/



### 使用ssh

```html
ssh-keygen

cd /home/matt/.ssh
    
ssh-copy-id -i id_rsa.pub root@192.168.96.128
```



```java
scp a.txt root@192.168.96.128:/home/a/b
```



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201222135659.png)



以管理元打开一直yes即可

**ssh-host-config**



passwd matt

matt





