## 安装

### 安装

[go 1.13.13](https://golang.org/dl/)

x86-64    



![](https://raw.githubusercontent.com/matt17du/img/main/img/20210420150359.png)



一直下一步安装即可，更改路径即可；

默认进行了环境变量配置



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

