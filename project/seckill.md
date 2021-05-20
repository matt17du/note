令牌桶 秒杀



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223104128.png)



限制某一秒网络的最大值

漏桶

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223104306.png)



平滑流量



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223105022.png)





总维度：各个接口总的维度



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223104939.png)









![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223105944.png)





## 开发模型

前后端分离，

后端：控制层、业务层、数据访问层

ViewObject:返回给前端的对象

Model:业务层使用的对象

DataObject:数据访问层使用的对象

前端的请求发给控制器，控制器调用业务层，业务层调用数据访问层



## 用户



### 用户注册

用户输入手机号，点击发送验证码，后端会生成验证码，redis保存一封，并发送给前端。用户提交注册信息，后端首先对验证码进行校验，之后生成用户model对象发送给业务层，业务层首先对数据进行校验，添加用户信息，用户密码。

// 用户表和用户密码表



### 用户登录

前端提交手机号和密码，后端首先校验数据，根据手机号查询用户信息，根据用户ID，查询密码，判断手机号密码是否匹配，匹配成功会在redis保存登录的token,并把token返回给前端。



### 根据ID查询用户



### 生成验证码

六位随机数



## 商品

### 创建商品

商品数据的校验->商品表、商品库存表添加数据



### 查询商品

首先从缓存中有没有，若没有则需要从数据库中查询，更新缓存->返回给用户



## 订单

### 创建订单

在用户点击下单时会需要输入验证码，由后端判断用户是否登录，登录则生成验证码图片并返回给前端，验证码也会在redis进行存储。

在用户点击验证时会验证验证码是否正确，用户是否存在，活动是否有效，之后会进行初始化流水状态，记录商品的初始化状态，消息队列发送一条消息，消息内容，商品ID，数量，商品日志ID



```
transactionalAsyncSendCreateOrder
```



```python
transactionMQProducer.setTransactionListener
     
public LocalTransactionState executeLocalTransaction
     
调用业务层创建订单
     
     
public LocalTransactionState checkLocalTransaction(MessageExt messageExt)
一直轮询的方式判断订单是否创建成功，通过检查商品日志表中的商品状态
     
     

```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225110322.png)

如果没有明确告诉你数据库是否执行成功就会一直调用check方法



校验用户商品活动库存是否合法，减库存，订单入库，更新销量，更新商品日志



生成订单号：时间，sequence获取当前值





等所有完成后发送消息，数据库提交才发送消息



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225104347.png)



## 活动

### 发布活动

根据商品ID生成活动，并把活动插入数据库中，将库存添加到redis中



### 生成活动token

用户商品活动校验之后生成token，保存在redis中 



## 表的设计



用户 用户密码

商品-》商品库存

商品库存日志

活动

序列化信息表

订单





## 错误



### 跨域



```java
//origins:服务器可以接受来自哪些域的请求
// allowCredentials: Access-Control-Allow-Credentials 响应头表示是否可以将对请求的响应暴露给页面。返回true则可以，其他值均不可以。
@CrossOrigin(origins = {"*"},allowCredentials = "true")
```



### 缓存



### 查询活动错误







使用行锁

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210224101303.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210224101427.png)





将库存缓存到redis中



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210224104300.png)





























![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225102841.png)

























活动校验、异步更新销量、记录商品的流水状态



























































![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225113257.png)































![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225133725.png)







![](https://raw.githubusercontent.com/matt17du/img/main/img/20210225134111.png)







