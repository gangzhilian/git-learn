# Git
## 初级
### git bash
* 相当于cmd
### 创建名字和邮箱
* git config --global user.name "Your Name"
* git config --global user.email "email@example.com"
### 创建版本库
* 创建文件夹
### 基础命令
* 基础命令和linux差不多
* git init:把文件夹设置成仓库
* git add:添加文件到仓库
    * git commit可以一次提交多个文件，一个一个的add文件
* git commit:把文件提交到仓库，其中 -m 后接提交的描述
    * 修改后，也需要git add和git commit
* git status:现在仓库的状态
* git diff 文件名:可以查看更新了什么
* git log:查看git历史日志
    * 使用--pretty=oneline参数进行输出简化
* 回退版本(仅仅是把指针指向需要的版本)
    * git reset --hard HEAD^ (一个^是上一个版本，两个^是上两个版本，过多就是~~次数)
    * 回到哪个版本  git reset --hard 版本号前几位
* git reflog:能查看回退的版本
### 库
* 构成
    * 工作区
    * 版本库(.git)
        * 暂存区:最重要的是index(stage)
        * 分支
        * 指向分支的指针
* 工作原理
    * git add 是把文件提交暂存区
    * git commit是把暂存区的提交到当前分支
### 修改
* 跟踪管理的是修改
* 撤销修改
    * 如果还没有add到暂存区，使用git checkout -- file
    * 如果添加到了缓存区，使用git reset HEAD file (回到工作区，HEAD表示最新的版本)
* 删除
    * 删除文件后，不论是手动还是rm，需要把版本库中的文件使用git rm 文件名删除，再提交同步
    * git checkout 是使用版本库文件替换工作区文件
### 远程仓库
* 创建ssh密钥
    * ssh-keygen -t rsa -C "youremail@example.com"
* 把id_rsa.pub中的密钥添加到github中
* 添加
    * 在github上创建新的仓库的话，会有指引
    * git push -u origin master
        * 当中-u参数是把本地master和远程master关联起来
    * 以后每次修改后，就可以使用git push origin master推送到远程库
    * 第一次添加有ssh警告是正常的
* 克隆
    * 使用git clone 就可以克隆远程仓库到本地
### 分支
* HEAD指向的是master，而master指向的是提交
* 命令
    * 创建分支就是增加一个新的指针，然后改变HEAD的指向
    * 创建分支:git checkout -b 分支名
        * checkout -b相当于 git branch 分支名来创建分支，然后checkout 切换分支
    * git branch:查看当前分支
    * git merge 分支名:合并分支到当前分支
    * git branch -d 分支名:删除分支
    * git branch -D 分支名:强制删除未合并的分支
* 冲突
    * 使用cat查看直接就可以查看到冲突位置
    * 使用git log --graph --pretty=oneline --abbrev-commit也可以查看到分支合并情况
    * 修改成一致就好
* 不使用fast forward
    * 在合并的使用--no-ff这个参数 再加-m(因为不适用fast forward模式合并会产生一个commit)进行合并
    * 这样就会看到历史合并，而使用fast forward不会看到历史合并
* 隐藏
    * 如果手头有工作，又需要在别的分支做别的工作，使用git stash把工作现场先隐藏起来
    * git stash list查看隐藏工作的列表
    * 恢复
        * 多步恢复
            * git stash apply
                * 恢复工作
            * git stash drop
                * 删除隐藏的工作
        * git stash pop
            * 恢复后把文件也删除
* 多人
    * git remote可以查看远程仓库的信息(-v可以查看更详细的信息)
    * 在本地创建和远程分支对应的分支，使用git checkout -b branch-name origin/branch-name
    * 建立本地分支和远程分支的关联，git branch --set-upstream branch-name origin/branch-name
    * 抓取分支git pull
    * git rebase:把git log整理成直线
### 标签
* git tag 标签名:创建标签
* 要是给过去的分支加标签 后面加commit id
* -d 删除标签
* git push origin 标签名:推送标签到远程仓库
* git push origin --tags:推送本地所有的标签

*XMind: ZEN - Trial Version*