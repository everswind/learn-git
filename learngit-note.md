# Git学习笔记
## Git简介
* Git是分布式版本控制系统
* 集中式VS分布式：  

   1）集中式版本控制系统，版本库集中存放在中央服务器，必须要联网才能工作,没有历史版本库。  
   
   2）分布式版本控制系统，没有“中央服务器”，每个开发人员电脑上都有一个完整的版本库。  
   
   3）分布式优势：安全性更高，不需要联网，如果“中央服务器”故障，任何一个其他开发人员的本地都有最新的带有历史记录的版本库。  
   
   4）主要区别在于历史版本库的存放，集中式历史版本只存在于中央服务器，而分布式中每个本地库都有历史记录存放。
## 安装Git
# Git命令
****
## Git配置
``` 
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
**注意**  `--global`参数表示你这台机器上所有的Git仓库都会使用这个配置。
## 创建版本库
#### 选择一个合适目录
1. 如`$ cd d:`
2. `$ mkdir <repository-name>`，创建库名
3. `$ cd <repository-name>`，进入库内  

**补充**  `pwd`显示路径，`ls`显示当前目录，`ls -ah`显示隐藏目录
#### 在当前目录初始化库
```
$ git init
```
## 使用vim编辑器
1. `$ vi <file-name>`，新建或修改文件
2. 按`i`进入编辑
3. 编辑完成后按`ESC`，然后选择以下某个命令输入

|命令|效果|
|--|--|
|:w|保存文件，不退出vi|
|:w \<file-name> |另存为file,不退出|
|:w!|强制保存，不退出|
|:wq|保存文件，退出|
|:wq!|强制保存，退出|
|:q|不保存，退出|
|:q!|不保存，强制退出|
|:e!|放弃所有修改，回到上次保存文件开始编辑|
## 把文件添加到版本库
```
$ git add <file-name>
$ git commit -m "description"
```
**注意**  可以多次`git add `，最后一次`git commit`
## 查看工作区当前状态
```
$ git status
```
## 时光穿梭
```
$ git reset --hard commit-id
``` 

**确定版本回退commit-id**  

`$ git log`，查看提交历史；`$ git log --pretty=oneline`，简化显示；按`q`退出查看  
  
`HEAD`，当前版本  

`HEAD^`，上个版本  

`HEAD^^`，上上个版本  

`HEAD~100`，往上100个版本

**确定重返未来commit-id**  

`$ git reflog`，查看命令历史
## 工作区与暂存区
![](https://camo.githubusercontent.com/14659c736537a60e9cf0076be119e14ef3cb089a/68747470733a2f2f63646e2e6c69616f78756566656e672e636f6d2f63646e2f66696c65732f6174746163686d656e74732f30303133383439303737303239313733343637323965396166626634313237623664666261653932303761663031363030302f30)  

   工作区就是电脑中能看到的目录，工作区有一个隐藏目录`.git`，这是Git的版本库  

  `$ git diff`，比较工作区与暂存区（即上次git add的内容）的不同，`$ git diff <file-name>`，比较具体文件的不同  

  `$ git diff --staged`或`$ git diff --cached`，比较暂存区与仓库分支（上次git commit）的不同
## 撤销修改
* 场景1——工作区已修改但未`git add`到暂存区  

  `$ git checkout -- <file name>`，其实就是用版本库里的版本替换工作区的版本
* 场景2——工作区修改且已经`git add`到暂存区，分两步  

  先`$ git reset HEAD <file name>`回到场景1，再按场景1操作
* 场景3：已经`commit`但没有推送到远程库——**版本回退**
## 删除文件
假设文件原已`commit`，目前情况——已经在目录下手动删除或`$ rm <file name>`  

选择一：确实要从版本库中删除该文件，分两步  

`$ git rm <file-name>`或`git add <file-name>`  

`$ git commit -m "message"`  

选择二：删错了，要恢复  

`$ git checkout -- <file name>`，其实就是用版本库里的版本替换工作区的版本
## 远程仓库
#### 创建SSH Key
```
$ ssh-keygen -t rsa -C "youremail@example.com"
```  

**补充**  在用户主目录下(`cd`)  

`$ ls -ah`可见`.ssh`目录  

`$ cd .ssh`可见`id_rsa`(私钥不能泄露)和`id_rsa.pub`(公钥可公开)
#### 关联远程仓库
```
$ git remote add origin git@github.com:username/repositoryname.git
```
或
```
$ git remote add origin https://github.com/username/repositoryname.git
```  
远程库默认名字为`origin` 
#### 推送到远程仓库
* 第一次推送到GitHub  
```
$ git push -u origin master
```
推送master分支
* 后续推送
```
$ git push origin master
```
不再使用参数`-u`
#### 从远程库克隆
```
$ git clone git@github.com:username/repositoryname.git
```  
或  
```
$ git clone https://github.com/username/repositoryname.git
```
## 分支管理
#### 查看分支
```
$ git branch
```
#### 创建分支
```
$ git branch <branch-name>
```
#### 切换分支
```
$ git checkout <branch-name>
```
#### 创建+切换分支
```
$ git checkout -b <branch-name>
```
#### 合并某分支到当前分支
```
$ git merge <branch-name>
```
#### 普通模式合并分支
```
$ git merge --no-ff -m "description" <branch-name>
```  
通常进行分支合并时，如果可以，Git会使用`Fast forward`模式，删除分支后，分支历史信息会丢失  

`--no-ff`表示禁用`Fast forward`模式，能看出曾做过合并
#### 删除分支
```
$ git branch -d <branch-name>
```
#### 强行删除分支
```
$ git branch -D <branch-name>
```
#### 查看分支合并图
```
$ git log --graph
```  
`$ git log --graph --pretty=oneline --abbrev-commit`，简洁查看
### Bug分支
假设场景——设A为游戏软件  

1. master 上面发布的是A的1.0版本
2. dev 上开发的是A的2.0版本
3. 这时，用户反映 1.0版本存在漏洞，有人利用这个漏洞开外挂
4. 需要从dev切换到master去填这个漏洞，正常必须先提交dev目前的工作，才能切换
5. 而dev的工作还未完成，不想提交，所以先把dev的工作stash一下。然后切换到master
6. 在master建立分支issue101并切换
7. 在issue101上修复漏洞
8. 修复后，在master上合并并删除issue101
9. 切回dev，恢复原本工作，继续工作
#### 保存工作现场
```
$ git stash
```
#### 查看保存的工作现场
```
$ git stash list
```
#### 恢复工作现场
```
$ git stash apply
```
#### 删除工作现场
```
$ git stash drop
```
#### 恢复并删除工作现场
```
git stash pop
```
### Feature分支
每添加一个新功能，最好新建一个feature分支，在上面开发完成后，合并，最后，删除该feature分支
## 多人协作
#### 查看远程库信息
```
$ git remote`或`git remote -v
```
#### 本地推送分支
```
$ git push origin <branch-name>
```
#### 在本地创建和远程分支对应的分支
```
$ git checkout -b <branch-name> origin/<branch-name>
```
#### 建立本地分支和远程分支的关联
```
$ git branch --set-upstream <branch-name> origin/<branch-name>
```  
或  
```
$ git branch --set-upstream-to=origin/<branch-name> <branch-name>
```
#### 从远程抓取分支
```
$ git pull
```
#### 多人协作通常的工作模式
1. 先试图推送自己的修改`git push`
2. 若推送失败，则远程分支比本地分支更新，`git pull`拉取远程分支试图合并
3. 若合并有冲突，则解决冲突，并在本地提交(`add` 和 `commit`)
4. 若没有冲突或解决了冲突，再次推送`git push`
## Rebase
“变基”  
```
$ git rebase
```  
只对尚未推送或尚未分享给别人的本地修改执行变基操作清理历史，从不对已推送至别处的提交执行变基操作
## 标签管理
发布一个版本时，我们通常先在版本库中打一个标签（`tag`），这样，就唯一确定了打标签时刻的版本  

将来无论什么时候，取某个标签的版本，就是把那个打标签的时刻的历史版本取出来。所以，标签也是版本库的一个快照
#### 创建标签
```
$ git tag <tag-name>
```
在最新commit上打一个标签  
```
$ git tag <tag-name> commit-id
```
在对应的commit_id上打一个新标签
#### 创建带有说明的标签
```
$ git tag -a <tag-name> -m "description" commit-id
```
`-a`指定标签名，`-m`指定说明文字  
#### 查看所有标签
```
$ git tag
```  
#### 查看对应标签的信息
```
$ git show <tag-name>
```
**注意**标签总是和某个commit挂钩。如果这个commit既出现在master分支，又出现在dev分支，那么在这两个分支上都可以看到这个标签。
### 操作标签
#### 推送某个标签到远程
```
$ git push origin <tag-name>
```
#### 一次性推送全部尚未推送的标签到远程
```
git push origin --tag
```
#### 删除一个本地标签
```
$ git tag -d <tag-name>
```
#### 删除一个远程标签
```
$ git tag -d <tag-name>
```
先从本地删除  
```
$ git push origin :refs/tags/<tag-name>
```
再从远程删除




