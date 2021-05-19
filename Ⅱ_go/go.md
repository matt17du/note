## 安装

### 安装

[go 1.13.13](https://golang.org/dl/)

x86-64    



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210420150359.png)



选择[go1.13.13.windows-amd64.msi](https://golang.org/dl/go1.13.13.windows-amd64.msi)一直下一步安装即可，更改路径即可；

或者选择[go1.13.13.windows-amd64.zip](https://golang.org/dl/go1.13.13.windows-amd64.zip)zip解压缩。





### 配置







设置国内镜像

```go
go env -w GOPROXY=https://goproxy.cn,direct
```

go的依赖管理

```go
go env -w GO111MODULE=on
```









```go
go get -v golang.org/x/tools/cmd/goimports 
```







GOROOT:指定go的安装目录

Path:指定go的安装目录下的bin目录

GOPATH:工作目录，go项目的工作目录



GOROOT

```
D:\develop\env\go
```

Path

```
%GOROOT%\bin
```

GOPATH

```
D:\matt\workspace\go
```











### 验证

验证go环境是否安装成功

```bash
go version
```

