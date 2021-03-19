

## 安装

[nodejs](https://nodejs.org/en/download/)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231171700.png)



**下载安装选择next即可**



## 更改安装目录



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231171737.png)



```java
node_cache
node_global
```

手动更改

```java
C:\Users\Administrator\.npmrc
```

文件，在记事本中打开，内容如下：

```java
prefix=D:\develop\env\nodejs\node_global
cache=D:\develop\env\nodejs\node_cache
```

这样就ok了



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231171810.png)

```java
prefix=D:\develop\env\nodejs\node_global
cache=D:\develop\env\nodejs\node_cache
```

**是\不是/**



## 配置环境变量



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231172047.png)



新建NODE_PATH

```java
NODE_PATH
```

```java
D:\develop\env\nodejs\node_global\node_modules
```





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231172010.png)





将其中默认的**C:\Users\用户名\AppData\Roaming\npm**更改为下图



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231171931.png)

## 更换镜像

1.更换网址

```java
npm config set registry https://registry.npm.taobao.org
```

恢复

```java
npm config set registry https://registry.npmjs.org
```

2.使用cnpm

```java
npm install -g cnpm --registry=https://registry.npm.taobao.org
```







## 测试



我们先安装一个express模块试试，打开dos命令窗口，执行下面的命令

```
npm install express -g      # -g  是全局安装的意思
```





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201231171842.png)

## 常见的命令

npm 常用的命令

1. npm -v 查看npm 当前安装的版本

2. npm init 初始化一个package.json 文件

3. npm install <module name> 安装一个依赖包 , 简写 npm i 

4. npm inistall --save <module name>  将安装的包添加到package.json的依赖中

5. npm inistall -g <module name> 全局安装一个包，一般安装的工具包 。比如：npm i -g express

6.npm docs <module name> 查看包文档

7.npm list 查看当前目录下安装的所有的包

8.npm list -g 查看全局安装包路径下的所有包

9.npm unistall <module name> 卸载当前目录下的某个包， 简写

10. npm uninstall --global <module name> 卸载全局安装目录下的某个包, 简写： npm i -g 

11. npm update <module name> 更新当前目录下的某个包

12. npm update -g <module name> 更新全局目录下的某个包

13. npm --help 可查看所有命令 简写：npm -h 

   npm help <common> 查看某条命令的详细帮助 npm help inistall 

14. npm i --save-dev 安装到开发环境，简写： npm i -D

15. npm view xxx version 查看当前包的版本信息

```
npm view css-loader version //3.5.2
npm view css-loader versions //查看所有的版本信息
```





安装webpack

```js
npm install webpack -g
```



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210319233446.png)



