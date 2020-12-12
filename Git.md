## Git

1.failed to push some refs to 'git@github.com:pavi-du/note.git'

问题：自己在远程仓库更改了内容，而本地不知道，直接提交

解决：

```
// git fetch+merge
git pull origin master 
```



```xml
// 第一下克隆下来
git clone https://github.com/matt17du/note.git
git remote -v
// 设置别名
git remote add origin https://github.com/matt17du/note.git
// 拉取
git pull origin
// 推送
git push origin master
```

// 注意分支

```git
git branch test

git branch -v

git checkout test

git merge test
```

