令牌桶





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223104128.png)



限制某一秒网络的最大值





漏桶



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223104306.png)





平滑流量







tps qps



维度



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223105022.png)





总维度：各个接口总的维度





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223104939.png)









![](https://raw.githubusercontent.com/matt17du/img/main/img/20210223105944.png)







用户注册



生成验证码

Random生成6位随机数，保存在在redis中，在用户注册页面提交注册信息，







登录

用户名密码校验后无误后生成token，存储在redis中并返回给前端

