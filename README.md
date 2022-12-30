# gitstudy
1: 基本操作

当前目录  ： git init 
看当前是空的： git status
将当前目录所有文件commit 到git 仓库   : git add .
需要commit : git commit
还需要配置邮箱 :  git config --global user.email "chenshoujin@keawave.com"
配置一个用户名字： git config --global user.name "jime chen"
如果我们要修改git commit 的编辑器 ： git config --global core.editor vim

如果不小心git commit 不需要的到仓库， 使用 git restore --staged . 取消当前目录所有文件
这样，刚才误操作的，就可以取消掉。

同时使用 .gitinore 控制不放到仓库里面
同时使用 git ls-files 查看有哪些文件是提交到仓库里面了
我们可以对提交的文件，进行commit ： git commit -m "sniofnasieofn"


分支控制

git branch
创建新的分支 ： 
git checkout -b rv64
分支切换 ： git checkout master

 
如果想将rv64分支合并到master 主分支上 ： git merge rv64
如果合并的rv64分支没有用了，我们就可以把他删除掉  ： git branch -d rv64



这里介绍如何把本地仓库推送到 github 远程仓库 ：

git remote add origin git@github.com:jimechang/gitstudy.git
我们把本地仓库推送到远程仓库 ： git push -u origin master
这里会报错，因为public key 的原因，因为远程仓库不知道本地仓库的秘钥，所以报错，我们需要将本地的秘钥告诉远程的仓库
首先查看本地秘钥 ： ls ~/.ssh ; 是否有 ID开头的秘钥，如果没有，我们新建秘钥
ssh-keygen -t ed25519 -C "chenshoujin@keawave.com"

生成后， 用 ls ~/.ssh 就可以看到新生成的秘钥对 ， pub后缀的是公钥，而私钥是不能告诉任何人的
我们将公钥上传。首先复制公钥 ： cat ~/.ssh/id_ed25519.pub

我们把本地仓库推送到远程仓库 ： git push -u origin master


注意：我们提交采用的SSH 协议， 而不是 url （https 协议）；如果提交错了，就需要先转换成 ssh 协议 ：
 git remote set-url origin git@github.com:jimechang/gitstudy.git


git remote rename <old> <new>   对远程仓库的进行重名
git remote remove <name>   移调远程仓库的名





对提交的文件的对比 ：  git diff HEAD* HEAD
                       git diff HEAD*

或者和cached的对比 ， git diff --cached HEAD*   ; git diff --cached

如果对当前工作区修改后进行存储，  git stash 
这个命令是把修改的放到一个堆栈里面。 所以你在 创建一个新的分支的时候，那么再用 git stash pop 进行取出来


还有如果你对一个文件多次修改，你又不想重复提交 ： 你可以  ：  git commit --amend -m 'same commit here'
这样就只产生一次提交

但是如果我发现重复提交里面有我需要的，想pop 出来，你可以使用 重置 ：
git reflog 查看我的提交 的东西

git reset id --hard   
这里的id 就是 一个标识数字



