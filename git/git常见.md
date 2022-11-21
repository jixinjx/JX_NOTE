## 代码提交到远程仓库
1：建立本地Git仓库

```
git init
```

2. 将所有项目文件添加到缓存中

```
git add.
```

3.将上述文件Commit到Git库中

```
git commit -m "XXXX"
```

4.将本地的git库远程连接到远程上

```
git remote add origin url
```

5.先将远程库中的redame.md下载下来

```
git pull --rebase origin master
```

6.然后将代码提交到远程库

```
git push origin master
```



## git切换远程地址

1：切换到远程仓库地址

 git remote set-url origin URL   --URL为新地址

2：先删除远程仓库地址，然后在添加

git remote rm origin 删除现有的远程仓库

git remote add origin url 添加新远程仓库

3：然后在查看现有的远程仓库地址

git remote -v



## Git创建分支，并将代码提交到分支上

**查看分支类型**

1.查看分支

```
$ git branch
* master
```

*标识为当前所在的分支

2：查看远程分支

```
$ git branch -r
```

3:查看所有分支

```
$ git branch -a
```

**本地创建分支**

```
$ git branch [分支名称]` `git branch newbranch
```

　　

**切换到新的分支**

```
git checkout newbranch
```

**创建并切换分支**

```
$ git checkout -b newbranch
```

上面一步为：本地创建分支和切换到新的分支结合

 

**将分支推送到远程服务中**

```
$ git push origin newbranch
```

**删除本地分支**

```
$ git branch -d newbranch
```

删除分支之前，先切换到主分支上

**删除远程分支**

```
$ git push origin :newbranch
```

**Git提交本地代码到新分支**

1.切换到新的分支

```
$ git checkout newbranch
```

2.添加本地代码

```
$ git add .
```

3.提交本地代码

```
$ git commit -m "add my new project"
```

4.提交到远程仓库中

```
$ git push origin newbranch
```

## 远程分支拉取最新代码合并到本地分支上

第一种方式：

```
//获取最新代码到本地

$ git fetch origin master  [获取远程的origin/master分支]

$ git fetch origin newbranch [获取远程的origin/dev分支]

//查看版本差异

$ git log -p master..origin/master [查看本地master与远程origin/master的版本差异]

$ git log -p newbranch..origin/newbranch [查看本地newbranch与远端origin/newbranch的版本差异]

//合并最新代码到本地分支

$ git merge origin/master  [合并远程分支origin/master到当前分支]

$ git merge origin/newbranch [合并远端分支origin/newbranch到当前分支]

//完成后提交

$ git push

//git  pull(拉取)  即从远程仓库抓取本地没有的修改并【自动合并】到远程分支     git pull origin master

//git  fetch(提取) 从远程获取最新版本到本地不会自动合并   git fetch  origin master
```



第二种方式：



```
//确认代码无误后提交到主分支

$ git checkout master //切换到主分支

$ git pull origin newbranch //把分支上的代码pull下来

$ git push //提交代码
```

## git如何把分支代码合并到master主分支上

1.切换到分支

```
$ git checkout newbranch
```

2.把分支代码pull下来

```
$ git pull

//或者

$ git pull origin newbranch
```

3.切换到主分支

```
$ git checkout master
```

4.把分支代码merge到主分支

```
$ git merge newbranch
```

\5. 把代码推送上去，然后分支代码就会合并到主分支上

```
$ git push 

//或者

$ git push origin master
```
