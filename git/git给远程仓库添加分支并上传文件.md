## 添加分支
1.初始化仓库
git init
2.创建并命名分支
**git checkout -b** 你的分支名字
3.将文件提交至暂存区
git add .
4.
git commit -m '本次提交备注信息'

5.连接远程仓库
git remote add origin 你的SSH地址
6.将文件提交至分支仓库
git push origin 你的分支仓库名字

## 合并分支
1、目标：将dev分支合并到master分支
1.1、首先切换到master分支上
git checkout master
1.2、如果是多人开发的话 需要把远程master上的代码pull下来
git pull origin master
//如果是自己一个开发就没有必要了，为了保险期间还是pull
1.3、然后我们把dev分支的代码合并到master上
git merge dev 
//如果有冲突，手动解决冲突就行。

1.4、然后查看状态及执行提交命令
git status

## 提示 fatal: refusing to merge unrelated histories 
将仓库中的 f01分支合并到master分支时，提示 fatal: refusing to merge unrelated histories 。此时需要在 git merge 后面加上  

--allow-unrelated-histories 。如下

将f01分支合并到master分支中
$  git checkout  master
$  git merge f01 --allow-unrelated-histories
