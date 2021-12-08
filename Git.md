```git
#安装git
git config --global user.name "Your name"
git config --global user.email "email@example.com"
```

```git
#新建仓库repository
git init
#将文件添加到仓库中
git add file_name
#将文件提交到仓库中
git commit -m "xxx"
#查看仓库当前状态，是否有文件被修改过，未提交
git status
#查看文件修改的具体内容
git diff file_name
#查看从最近到最远的提交日志,每次提交会有一个commit id
git log
git log --pretty=oneline
#版本回退
HEAD 当前版本
HEAD^ 上一版本
HEAD^^ 上上一版本
HEAD~100 往上100个版本
git reset --hard HEAD^
#版本回退会将日志中当前版本删去，但通过其commit id回到这个版本
#commit id没有必要写全
git reset --hard a2681
#查看命令历史
git reflog
```

```git
#撤销修改
场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。
    命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：
    一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；
    一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。
    总之，就是让这个文件回到最近一次git commit或git add时的状态。

场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令git reset HEAD <file>，就回到了场景1，第二步按场景1操作。

场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。
```

```git 
#删除文件
一：在工作区删除文件后，删除版本库中的文件
git rm file_name
git commit
二：在工作区删除文件后，属于误删恢复文件
git checkout -- file_name
```

```git
#远程仓库
#本机生成ssh key
ssh-keygen -t rsa -C "youremail@example.com"
#关联远程库
git remote add origin git@github.com:279804711/learngit.git
#将本地库里的文件推送到远程库
由于远程库是空的，我们第一次推送master分支时，加上了-u参数，Git不但会把本地的master分支内容推送的远程新的master分支，还会把本地的master分支和远程的master分支关联起来，在以后的推送或者拉取时就可以简化命令。
git push -u origin master
#本地master分支的最新修改推送至GitHub
git push origin master
#删除远程库
git remote rm <name>
#查看远程库信息
git remote -v
#从远程库克隆
git clone git@github.com:michaelliao/gitskills.git
```

```git
#分支管理
#创建分支
git checkout -b dev
#创建并切换
git branch dev
git checkout dev
#查看当前分支
git branch
#将分支dev合并到master分支上去
git merge dev
#删除分支
git branch -d dev

创建并切换到新的dev分支，可以使用：
git switch -c dev
直接切换到已有的master分支，可以使用：
git switch master

#解决冲突，手动解决冲突后，提交
#查看分支
git log --graph

#分支管理策略
#不采用fast forward进行合并分支
git merge --no-ff -m "xxx" <branch_name>

#Bug分支
#保存工作区现场
git stash
#查看保存列表
git stash list
#恢复工作区现场
一：
git stash apply
git stash drop
二：
git stash pop
三：指定恢复
git stash apply stash@{0}
#将bug解决完后的主分支的修改“复制”到dev分支
在master分支上修复的bug，想要合并到当前dev分支，可以用git cherry-pick <commit>命令，把bug提交的修改“复制”到当前分支，避免重复劳动。
```

