### 安装

解压配置即可

```
tar -zxvf xxx.tar.gz
```





1.max file descriptors [4096] for elasticsearch process is too low, increase to at least [65536]

　　每个进程最大同时打开文件数太小，可通过下面2个命令查看当前数量

```
ulimit -Hn
ulimit -Sn
```

　　修改/etc/security/limits.conf文件，增加配置，用户退出后重新登录生效

```
*               soft    nofile          65536
*               hard    nofile          65536
```

2、max number of threads [3818] for user [es] is too low, increase to at least [4096]

　　问题同上，最大线程个数太低。修改配置文件/etc/security/limits.conf（和问题1是一个文件），增加配置

```
*               soft    nproc           4096
*               hard    nproc           4096
```

　　可通过命令查看

```
ulimit -Hu
ulimit -Su
```

3.max virtual memory areas vm.max_map_count [65530] is too low, increase to at least [262144]

　　修改/etc/sysctl.conf文件，增加配置vm.max_map_count=262144

```
vi /etc/sysctl.conf
sysctl -p
```

　　执行命令sysctl -p生效

4.Exception in thread "main" java.nio.file.AccessDeniedException: /usr/local/elasticsearch/elasticsearch-6.2.2-1/config/jvm.options

　　elasticsearch用户没有该文件夹的权限，执行命令

```
chown -R es:es /usr/local/elasticsearch/
```

**查看当前用户的所在的组**

```
id matt # matt:用户名
```



vim jvm.options



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210118172546.png)

```c
-Xms512m
-Xmx512m
```

vim elasticsearch.yml



```c
bootstrap.memory_lock: false
bootstrap.system_call_filter: false
network.host: 0.0.0.0
cluster.initial_master_nodes: ["node-1"]
```

### 启动

```python
./elasticseach -d # 后台启动，没有-d则为前台启动
```

