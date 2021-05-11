font-family: JetBrains Mono; 



## iqbit

一直next安装即可(自定义安装可以修改安装位置)，之后把破解文件添加到安装目录下点击patch即可,不需要退出程序

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210108162544.png)



## switchhost

[官网](https://github.com/oldj/SwitchHosts/releases)





## sublime

### 安装pac

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201221220711.png)





### 插件

convert to utf-8

chinese :中文

**pac**

①安装package controll

②输入pac,选择install package controll回车即可



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201221220751.png)





![image-20201023000557995](D:\matt\workspace\git\app\img\image-20201023000557995.png)





![image-20201023000707096](D:\matt\workspace\git\app\img\image-20201023000707096.png)



![image-20201023000350172](D:\matt\workspace\git\app\img\image-20201023000350172.png)



### 更改插件目录的位置

 原目录删除，在安装目录下建立Data文件夹即可。



## fscapture

```
FastStone Capture(FSCapture) 注册码
2018年07月18日 15:19:08 殇莫忆 阅读数：12509
企业版序列号： 
name：bluman 
serial/序列号/注册码：VPISCJULXUFGDDXYAUYF 

FastStone Capture 注册码 序列号： 
name/用户名：TEAM JiOO 
key/注册码：CPCWXRVCZW30HMKE8KQQUXW 

USER NAME:TEAM_BRAiGHTLiNG_2007 
CODE:XPNMF-ISDYF-LCSED-BPATU 
```

推荐选择第一个

[官网](https://www.faststone.org/FSCaptureDetail.htm)

[中文官网](https://www.faststonecapture.cn/download)

## 7-zip



## IDM

idm 6.38

下载解压绿化即可



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210130103333.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210130103430.png)

## 图床

推荐[picgo](https://github.com/Molunerfinn/PicGo)





## cygwin

http://www.cygwin.com/

1.点击下图链接，下载安装包，点击安装包即可

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210129225052.png)







![](https://raw.githubusercontent.com/matt17du/img/main/img/20210129230335.png)





2、三种安装模式
①Install from Internet，这种模式直接从Internet安装，适合网速较快的情况；
②Download Without Installing，这种模式只从网上下载Cygwin的组件包，但不安装；
③Install from Local Directory，这种模式与上面第二种模式对应，当你的Cygwin组件包已经下载到本地，则可以使用此模式从本地安装Cygwin

**我们选择第一种**





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210129230453.png)





3、选择安装路径



软件安装的位置



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210129230650.png)





组件安装的位置





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210129230745.png)



4.代理

①Use System Proxy Settings 使用系统的代理设置
②Direct Connection 一般多数用户都是这种直接连接的网络，所以都是直接使用默认设置即可
③Use HTTP/FTP Proxy 使用HTTP或FTP类型的代理。如果有需要，自己选择此项后，设置对应的代理地址和端口，即可



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210129230909.png)





5、选择下载站点
不同的镜像存放了不同的包，为了获得最快的下载速度，我们可以添加网易开源镜像http://mirrors.163.com/cygwin/ 或者 阿里云镜像http://mirrors.aliyun.com/cygwin/



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210129231042.png)



6.组件的选择

此处，对于安装Cygwin来说，就是安装各种各样的模块而已。最核心的，记住一定要安装Devel这个部分的模块，其中包含了各种开发所用到的工具或模块

展开devel

从中选择binutils、 gcc 、mingw 、gdb进行安装，找到以下选项，点击后边的skip，使其变为版本号即可



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210129231329.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210129231447.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20210129231532.png)





点击下一步安装即可。





### 检验

检查是否安装成功

```c
cygcheck -c cygwin
```





### 添加右键

**Step 2 准备启动脚本**

- 以我的安装目录(d:\cygwin)为例
- 在d:\cygwin\bin\下准备一个启动脚本，命名为cygwin.bat
- 内容为：

```
@echo off
set _WindowsDIR=%*
D:\cygwin\bin\mintty.exe -i /Cygwin-Terminal.ico -

```

*如果出现最后出现闪退的情况，把最后一行改为"D:\cygwin\bin\mintty.exe" -i /Cygwin-Terminal.ico -*

Step 3 添加右键菜单

打开注册表编辑器，在计算机\HKEY_CLASSES_ROOT\Directory\Background\shell下新建项CygWin，将其默认字符串值改为CygWin Here(右键菜单显示的内容)
然后新建一个字符串值，名称改为Icon，字符串值改为D:\ProgramFiles\cygwin64\Cygwin.ico
之后为CygWin添加子项command，将默认字符串值改为D:\ProgramFiles\cygwin64\bin\cygwin.bat %V 如图



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210320000521.png)



- **Step 4 Cygwin获取环境变量**
- 编辑bash_profile：vim ~/.bash_profile
- 在最后添加内容:

```
if [[ $_WindowsDIR != "" ]]
then
	TMPDIR=${_WindowsDIR//\\//}
	unset _WindowsDIR
	cd "$TMPDIR"
fi


```



### jetBrains使用cygwin

![](https://raw.githubusercontent.com/matt17du/img/main/img/20210320213501.png)







## 窗口最大化

应用属性中选择











## pdman

数据库建模工具

[pdman](http://www.pdman.cn/#/)







## utools



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210331110807.png)





## powertoys













## **pdf相关**

### xodo

pdf阅读  













## chrome



[剪切板](chrome://flags/#clipboard-filenames)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210510104647.png)