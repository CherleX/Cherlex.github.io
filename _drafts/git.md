# Git 实用操作 #


## git init ##
> 初始化

```
git init

Initialized empty Git repository in E:/Code/test/.git/
```
## git remote add ##
> 添加远程仓库

```
git remote add origin git@code.huawei.com:z00291869/Demo.git
```

## git branch ##
> 指定远程跟踪分支

```
git branch --set-upstream-to master origin/master
```
## git clone ##
> 克隆远程仓库

```
git clone git@code.huawei.com:z00291869/Demo.git
```

## git commit ##
> 提交工作区修改内容，可以通过`-m`来指定comment

```
git commit -m "test"
```

## git push ##
> 指定推送到的远程分支

```
git push --set-upstream origin master
```

## git pull ##
> 取回远程某个分支的更新到本地分支

```
git pull origin master:master
```
> 如果是和当前分支合并，可以省略:后面的分支名

```
git pull origin master
```

> 如果当前分支已经追踪了远程分支，则可以省略远程分支名

```
git pull origin
```

> 如果当前分支只有一个追踪分支，则主机名也可以省略

```
git pull
```

## git checkout ##
> 可以用来创建本地新分支

```
git checkout -b test
```
> 也可以切换分支

```
git checkout test
```

> 也可以切换HEAD到特定的提交，比如切换到当前提交的祖父提交

```
git checkout HEAD~2
```

## git merge ##
> 合并一个本地分支，比如合并本地master分支到当前分支

```
git merge master
```

> 也可以合并远程分支

```
git mrege origin/master
```

## git reset ##
- --soft – 缓存区和工作目录都不会被改变
- --mixed – 默认选项。缓存区和你指定的提交同步，但工作目录不受影响
- --hard – 缓存区和工作目录都同步到你指定的提交


> 对于文件，reset命令可以把缓存区同步到指定的提交

```
git reset HEAD~1 test_test.test
```
> 一般来reset命令用来将文件从缓存区移除

```
git reset test.test
```


> 完全放弃工作区所有的修改

```
git reset --hard HEAD
```

> 放弃本地最后一次提交

```
git reset HEAD~1
```

## git revert ##
> 撤销已经提交的更改，可以理解为对某一个提交的反提交（比如，某次提交增加了某行代码，revert则删除某行代码，比如撤销当前提交的祖父提交

```
git revert HEAD~2
```
