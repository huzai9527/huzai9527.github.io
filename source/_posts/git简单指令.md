---
title: git简单指令
date: 2018-12-25 09:02:58
tags: git
---
# git简单指令
## 首先放一张学习路线
![git学习路线](Git.png)
## 1、创建版本库
```bash
mkdir huzai //创建一个空目录
cd huzai  //进入此目录
git init  //初始化git仓库
```
## 2、添加文件到版本库
```bash
git add file  //将文件添加到缓存区
git commit -m "post message" //提交并附带提交信息
```
## 3、版本回退
```bash
git reset --hard HEAD^ //HEAD是一个指针，指向当前的版本,^代表上一代版本，HEAD^^代表上两代
git reflog //查询每次提交的commit_id
git reset --hard commit_id //根据id进行回退
```
## 4、管理修改
```bash
git diff HEAD -- file //查看工作区（file）与最新版本（HEAD）的区别
```
## 5、撤销修改
```bash
git checkout -- file //直接丢弃工作区的修改（可用于恢复误删的文件）
//对于已经添加到缓存的修改
git reset HEAD file //撤销缓存区的修改
git checkout -- file 
```
## 6、删除文件
```bash
rm file //删除本地文件
git rm file //删除版本库中的文件
git commit -m "post delete" //提交删除事务
```
## 7、连接远程仓库
```bash
//先生成连接密钥
ssh-kengen -t rsa -C username
//将id_rsa.pub中的内容复制到github的密钥管理中
//再根据github的提示将本地仓库与远程仓库进行关联
git remote add origin git@github.com:username/repository
//再推送master分支的所有内容到远程仓库
git push -u origin master
```
## 8、从远程仓库进行下载
```bash
git clone git@github.com:username/repository
```
## 9、创建新的分支并切换到该分支下
```bash
git checkout -b branchname //创建并切换
git branch branch_name //创建
git checkout branch_name //切换
```
## 10、合并指定分支到当前分支
```bash
git merge branch_name
```
## 11、删除分支
```bash
git branch -d branch_name
```
## 12、如果合并时出现冲突
```bash 
cat conflic_filename
//git 会用<<<<< ===== >>>>>>显示不同分支的内容，你则需要手动解决冲突
```
## 13、分支管理策略
master分支应该是非常稳定的，也就是用于发布最新版本的，平时不应该在上面干活，干活都应该在dev分支上
也就是说dev分支是不稳定的，到了某个时候将dev分支合并到master分支上，你和你的小伙伴应该在各自的分支上干活，然后推送到dev分支上
## 14、bug分支
```bash
git add now_file
git stash //保护现场
//这里修改bug
git stash pop //提取现场，继续工作
```
## 15、丢弃一个没有被合并的分支
```bash
git branch -D branch_name 
```
## 16、多人协作
 1、尝试git push origin branch_name
 2、如果推送失败，说明远程分支比你的版本新，则你git pull 拉取远程文件
 3、合并你两的分支，如果有冲突则手动解决问题
 4、重复1
 - 注：如果git pull 提示 no tracking information 则说明远程分支和本地分支没有关联用下面的命令进行关联
```bash
git branch --set-uostream-to branch_name origin/branch_name
```
或者你不知道有什么分支
```bash
git remote -v //查看远程仓库的信息
git checkout -b branch_name origin/branch_name //创建本地分支以及远程分支
git branch --set-upstream-to branch_name origin/branch_name //进行关联
```
