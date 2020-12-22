## 概述

![image-20201221214158719](C:\Users\matt\AppData\Roaming\Typora\typora-user-images\image-20201221214158719.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201221215543.png)





概念模型



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220202232.png)







![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220202423.png)



message:消息





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220203132.png)











![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220203359.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220203700.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220203743.png)



## 安装

```
vim /etc/hosts
```

```
192.168.96.128 rocketmq-nameserver1
192.168.96.128 rocketmq-master1
```





```java
mkdir /usr/local/apache-rocketmq

tar -zxvf apache-rocketmq.tar.gz -C /usr/local/apache-rocketmq/
```





```java
cd /usr/local/apache-rocketmq/
    
ln -s apache-rocketmq/ rocketmq
```

```
mkdir /usr/local/rocketmq/store 
mkdir /usr/local/rocketmq/store/commitlog 
mkdir /usr/local/rocketmq/store/consumequeue 
mkdir /usr/local/rocketmq/store/index
```

```
vim /usr/local/rocketmq/conf/2m-2s-async/broker-a.properties
```



/2m-2s-async



broker-a.properties



```
#把下面得配置覆盖替换到broker-a.properties文件中
#所属的集群名字
brokerClusterName=rocketmq-cluster
#broker名字，注意：此处不同的配置文件填写的不一样
brokerName=broker-a
# 0 表示 master主节点 ，不是0则代表从节点slave
brokerld=0
#nameServer地址，分号分隔，
#注意：nameSeve的地址就是部署mq服务器的地址，可以在/etc/hosts中修改服务器ip指定一个名字
#我的服务器ip对应的名字是阿里云默认的名字aliyun
#也可以自己修改成名字叫rocketmq-nameserver1,修改方法为
#vim /etc/hosts ,然后保存退出，再重启一下网卡命令： service network restart
namesrvAddr=rocketmq-nameserver1:9876
#在发送消息时，自动创建服务器不存在的topic，默认创建的队列数
defaultTopicQueueNums=4
#是否允许broker自动创建topic,建议线下开启，线上关闭
autoCreateSubscriptionGroup=true
#broker 对外服务的监听端口
listenPort=10911
#删除文件时间点，默认凌晨4点
deleteWhen=04
文件保留时间，默认48小时
fileReservedTime=48
#commitlog每个文件的大小默认1G
mapedFileSizeCommitLog=1073741824
#ConsumeQueue每个文件默认存30w条，根据业务情况调整
mapedFileSizeConsumeQueue=300000
#检测物理文件磁盘空间
diskMaxUsedSpaceRatio=88
 
#存储路径
storePathRootDir=/usr/local/rocketmq/store
#commitlog 存储路径
storePathCommitLog=/usr/local/rocketmq/store/commitlog
#消费队列存储路径
storrPathConsumeQueue=/usr/local/rocketmq/store/consumequeue
#消息索引存储路径
storePathIndex=/usr/local/store/index
#checkpoint文件存储路径
storeCheckpoint=/usr/local/rocketmq/store/checkpoint
#abort文件存储路径
abortFile=/usr/local/rocketmq/store/abort
#限制消息得大小
maxMessageBiz=65536
#broker的角色
#ASYNC_MASTER 异步复制模式master
#SYNC_MASTER 同步双写模式master
#SLAVE
brokerRole=ASYNC_MASTER
#刷盘方式
#ASYNC_MASTER 异步刷盘
#SYNC_MASTER 同步刷盘
flushDiskType=ASYNC_FLUSH
```



```bash
mkdir -p /usr/local/rocketmq/logs 
cd /usr/local/rocketmq/conf && sed -i 's#${user.home}#/usr/local/rocketmq#g' *.xml
```

vim /usr/local/rocketmq/bin/runbroker.sh

```bash
JAVA_OPT="${JAVA_OPT} -server -Xms1g -Xmx1g -Xmn1g
```

vim /usr/local/rocketmq/bin/runserver.sh



```bash
JAVA_OPT="${JAVA_OPT} -server -Xms1g -Xmx1g -Xmn1g
```



cd /usr/local/rocketmq/bin/





```bash
nohup sh mqnamesrv &
```





**忘记指定IP**

```bash
nohup sh mqbroker -c ../conf/2m-2s-async/broker-a.properties >/dev/null 2 >&1 &
```



nameserver:用于协调

broker:服务器







## 生产者









![](https://raw.githubusercontent.com/matt17du/img/main/img/20201222204249.png)

主从模式：当主机写入数据时，从节点会拉取主节点的值







同步刷盘：



异步刷盘：直接返回成功，之后才判断数据是否存在





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201222204917.png)







```
sh mqshutdown broker
```

```
sh mqshutdown namesrv
```

