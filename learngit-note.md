# Git学习笔记
## Git是分布式版本控制系统
相对集中式版本控制系统有以下优点
* 无需联网
* 没有“中央服务器”，更安全
* 每个开发人员本地都有一个带有历史纪录的版本库
## 安装Git
## Git配置
``` 
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
```
**注意**  `--global`参数表示你这台机器上所有的Git仓库都会使用这个配置
## 创建版本库
1. 切换一个合适目录，如`$ cd d:`
2. `$ mkdir <repository-name>`，创建库名
3. `$ cd <repository-name>`，进入库内
4. `$ git init`，初始化库
   
**补充**  `pwd`显示路径，`ls`显示当前目录，`ls -ah`显示隐藏目录
## 使用vim编辑器
1. `vi <file-name>`，新建或修改文件
2. 按`i`进入编辑
3. 编辑完成后按`ESC`，然后选择以下某个命令

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
$ git commit -m "message"
```
**注意**  可以多次`git add `，最后一次`git commit`
## 查看仓库当前状态
`$ git status`
## 时光穿梭
`$ git reset --hard commit-id` 

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

  `$ git diff`，比较工作区与暂存区（即上次git add的内容）的不同，`$ git diff <file-name>`，比较具体文件的不同  

  `$ git diff --staged`或`$ git diff --cached`，比较暂存区与仓库分支（上次git commit）的不同

## 撤销修改
* 场景1——工作区已修改但未`git add`到暂存区  

  `$ git checkout -- <file name>`，其实就是用版本库里的版本替换工作区的版本
* 场景2——工作区修改且已经`git add`到暂存区，分两步  

  先`$ git reset HEAD <file name>`回到场景1，再按场景1操作
* 场景3：已经`commit`但没有推送到远程库——**版本回退**
## 删除文件
假设文件原已`commit`，目前情况——已经目录下手动删除或`$ rm <file name>`  

选择一：确实要从版本库中删除该文件，分两步  

`$ git rm <file-name>`或`git add <file-name>`  
`$ git commit -m "message"`  

选择二：删错了，要恢复  

`$ git checkout -- <file name>`，其实就是用版本库里的版本替换工作区的版本
## 远程仓库
### 创建SSH Key
`$ ssh-keygen -t rsa -C "youremail@example.com"`  

**补充**  

在用户主目录下(`cd`)  

`$ ls -ah`可见`.ssh`目录  

`$ cd .ssh`可见`id_rsa`(私钥不能泄露)和`id_rsa.pub`(公钥可公开)
### 关联远程仓库
`$ git remote add origin git@github.com:username/repositoryname.git`

或  

`$ git remote add origin https://github.com/username/repositoryname.git`  

远程库默认名字为`origin` 
### 推送到远程仓库
* 第一次推送到GitHub  

  `$ git push -u origin master`，推送master分支
* 后续推送  

  `$ git push origin master	`，不再使用参数`-u`
### 从远程库克隆
`$ git clone git@github.com:username/repositoryname.git`  

或  

`$ git clone https://github.com/username/repositoryname.git`

## 分支管理
### 查看分支
`$ git branch`
### 创建分支
`$ git branch <branch-name>`
### 切换分支
`$ git checkout <branch-name>`
### 创建+切换分支
`$ git checkout -b <branch-name>`




