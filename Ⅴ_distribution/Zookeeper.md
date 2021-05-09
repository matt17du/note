## 安装与使用

### 单点安装 

```
// 解压

// 修改配置文件
cd conf

cp zoo_sample.cfg zoo.cfg

vim zoo.cfg
```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201225202020.png)



```

// conf目录下
dataDir=/opt/zookeeper-3.4.10/zkData


cd ../

mkdir zkData
```



### 启动

```
./zkServer.sh start

```

进入客户端

```
./zkCli.sh
```

退出客户端

```
quit
```

关闭服务端

```
./zkServer.sh stop
```

### 集群安装



```
// 在zkData文件夹下
touch myid
```

编写服务器唯一标识

```
vim myid
```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201227002629.png)





```
server.A=B:C:D。

c:数据的复制使用的端口

d:发送选举信息使用端口
```

在zookeeper/conf/下的配置文件添加如下内容，之后启动即可

```
server.1=192.168.96.128:2888:3888
server.2=192.168.96.129:2888:3888
server.3=192.168.96.130:2888:3888
```

