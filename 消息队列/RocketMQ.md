

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220202232.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220202349.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220202423.png)







![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220203132.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220203336.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220203359.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220203700.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201220203743.png)



```java
mkdir /usr/local/apache-rocketmq

tar -zxvf apache-rocketmq.tar.gz -C /usr/local/apache-rocketmq/
```





```java
cd /usr/local/apache-rocketmq/
    
ln -s apache-rocketmq/ rocketmq
```







```java
nohup sh mqbroker -c /usr/local/rocketmq/conf/2m-2s-async/broker-a.properties  >/dev/null 2>&1 &
```

```java
nohup sh mqbroker -c /usr/local/rocketmq/conf/2m-2s-async/broker-a.properties  >/usr/local/rocketmq/logs/broker-a.log 2>&1 &
```

2m-2s-async



broker-a.properties