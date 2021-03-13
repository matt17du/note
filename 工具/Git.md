## 

1.failed to push some refs to 'git@github.com:pavi-du/note.git'

问题：自己在远程仓库更改了内容，而本地不知道，直接提交

解决：

```
// git fetch+merge
git pull origin master 
```



```xml

```

## 命令



### 基本

```java
// 第一下克隆下来
git clone https://github.com/matt17du/note.git
git remote -v
// 设置别名
git remote add origin https://github.com/matt17du/note.git
// 拉取
git pull origin
    
// git add --all
git add --all
    
git commit -m "xxxm"
    
// 推送
git push origin master:master
    

```



### 分支

```java
git branch // 查看本地分支

git branch -r // 查看远程分支

git branch -a // 查看本地分支和远程分支
    
git branch test // 创建test分支


git checkout test // 切换test分支

git merge test // 合并test分支
```



### SSH登录

```python
cd ~ # 进入家目录

rm -rvf .ssh # 删除.ssh 目录

ssh-keygen -t rsa -C matt17@qq.com # 运行命令生成.ssh 密钥目录
```



```python
cd .ssh

cat id_rsa.pub
```

复制 id_rsa.pub 文件内容，登录 GitHub，点击用户头像→Settings→SSH and GPG keys

New SSH Key

输入复制的密钥信息






## 错误

### 由于第一次使用不是git clone 然后直接推送



```java
git pull origin master --allow-unrelated-histories
// 合并俩个独立的仓库
```

IDEA如何第一次创建项目提交

首先在githup中创建项目



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201219202633.png)





![](https://raw.githubusercontent.com/matt17du/img/main/img/20201219202929.png)



之后的俩步

![](https://raw.githubusercontent.com/matt17du/img/main/img/20201219205240.png)









![](https://raw.githubusercontent.com/matt17du/img/main/img/20201219205341.png)



![](https://raw.githubusercontent.com/matt17du/img/main/img/20201219220054.png)





**这里记得和远程仓库的名字相同，如果远程是master,这里也得是master**



之后可能会出现 **Push rejected: Push to origin/master was rejected**



我们输入以下内容即可

```java
git pull origin master --allow-unrelated-histories
// master远程仓库分支名
```

紧接着add,commit,push即可



```
# IntelliJ project files
.idea
*.iml
out
gen

# Compiled class file
*.class
# Log file
*.log
# BlueJ files
*.ctxt
# Mobile Tools for Java (J2ME)
.mtj.tmp/

# Package Files #
*.jar
*.war
*.nar
*.ear
*.zip
*.tar.gz
*.rar
# virtual machine crash logs, see http://www.java.com/en/download/help/error_hotspot.xml
hs_err_pid*
.classpath
.project
.settings
target
.gitignore
```



