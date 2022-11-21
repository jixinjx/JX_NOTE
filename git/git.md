…or create a new repository on the command line
```
echo "# JX_NOTE" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/jixinjx/JX_NOTE.git
git push -u origin main
```

…or push an existing repository from the command line
git remote add origin https://github.com/jixinjx/JX_NOTE.git
git branch -M main
git push -u origin main
…or import code from another repository
<<<<<<< HEAD
You can initialize this repository with code from a Subversion, Mercurial, or TFS project.
=======
You can initialize this repository with code from a Subversion, Mercurial, or TFS project.


先说明一下https 和ssh-key. 拉取代码的区别

1.https://github.com/xxxx/xxxx.git  

灵活拉取代码，只是每次需要输入密码，并且安全性肯定没有ssh-key的高

2.git@github.com:xxxxxxxxx.git

如果你是固定电脑写代码，并且私有仓库，建议直接配置ssh-key，一劳永逸，配置一次就可以用了，ssh-key 生成的公钥 里面包含了本地电脑信息的  所以说配置了一次这台电脑就能一直用了

开始：
一、设置git的user name和email
如果你是第一次使用，或者还没有配置过的话需要操作一下命令，自行替换相应字段。

git config --global user.name "xxxx"
git config --global user.email  "xxxx@xxx.com"

说明：git config --list 查看当前Git环境所有配置，还可以配置一些命令别名之类的。

二、检查是否存在SSH Key
cd ~/.ssh
ls
或者
ll
//看是否存在 id_rsa 和 id_rsa.pub文件，如果存在，说明已经有SSH Key

1.存在ssh key（直接进行第三步）


2.不存在ssh key（即没有id_rsa和id_rsa.pub 文件）

如果没有SSH Key，则需要先生成一下

ssk-keygen 如果提示不存在 那么需要配置环境变量（path里面增加/git/bin），或者切换到git安装目录下面的bin文件夹下面去运行下面的命令

ssh-keygen -t rsa -C "xxx@xxx.com"  //刚才配置的邮箱地址

然后再次查看






三、获取SSH Key
cat id_rsa.pub
//拷贝秘钥 ssh-rsa开头. 复制下面这一长串的字符串  就是ssh key



四、GitHub添加SSH Key
GitHub进入个人中心，点击头像


新建一个SSH Key





取个名字。把上面的ssh-key 复制到这里就可以了 

五、验证和修改
测试是否成功配置SSH Key



 配置成功， 现在就可以进行用ssh 拉取代码了

git remote add origin  git@github.com:xxxxxxxxx.git

git pull 

git branch -a
 git checkout 20220916

## 拉取分支代码
git clone url -b branch
>>>>>>> init
