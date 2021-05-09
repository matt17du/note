

微服务架构是一种架构模式，它提倡将单一应用程序划分成一组小的服务，服务之间互相协调、互相配合，为用户提供最终价值。每个服务运行在其独立的进程中，服务与服务间采用轻量级的通信机制互相协作（通常是基于 HTTP 协议的 RESTful API) 。每个服务都围绕看具本业务进行构建，并且能够被独立的部署到生产环境、类生产环境等。







![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507143423.png)









![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507143756.png)







<img src="https://raw.githubusercontent.com/matt17du/img/main/img/20210507151323.png" style="zoom:900%;" />



**推荐使用：**

- nacos
- sentienl
- gateway









![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507153317.png)









![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507153847.png)



父工程删除src





在别的项目中下载lombok，因为depencyment并不引入



跳过测试

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507165150.png)











![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507165842.png)







![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507170030.png)









![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507192156.png)







先clean 后install

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210507204456.png)







注册中心：专家有几个，病人有几个





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210508100402.png)





**switchhost**

不要使用aa.com使用aa











```bash
Caused by: org.apache.zookeeper.KeeperException$UnimplementedException: KeeperErrorCode = Unimplemented for /services/cloud-provider-payment/27178f0f-2017-4893-b9a9-ece0b7628a98
```

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210509144653.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210509144802.png)





项目中3.5.3

linux中 3.5.0







### consul

开发模式下启动

```bash
consul agent -dev
```

