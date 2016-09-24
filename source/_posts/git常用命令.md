---
title: git常用命令
date: 2016-09-08 16:36:18
tags: "git"
---
#### 添加文件到仓库
	git add file
#### 提交文件到仓库
	git commit -m 'desc'
#### 显示当前仓库的状态
	git status
#### 显示仓库的提交日志
	git log --pretty=oneline

#### 回退版本
	git reset --hard HEAD^
	git reset --hard head~100 往回100个版本
	git reset --hard 08b8637 回退指定版本
#### 显示提交操作对应的版本
	git reflog
#### 复原工作区的文件（回到最近一次git commit或commit add）
	git checkout -- file
#### 撤销暂存区修改，重新放回工作区
	git reset head file
#### 从版本库删除文件
	git rm test.txt
	git commit -m 'del file'

#### 远程关联github
	git remote add origin git@github.com:dujiecn/learngit.git
#### 提交到远程仓库
	git push -u origin master
##### 拷贝远程仓库代码
	git clone git@github.com:dujiecn/gitskills.git
#### 查看最近一次提交的内容
	git log -n 1 --stat

### 创建一个tag标签
	
	git tag -a v3.0.0 -m '3.0.0版本'
	
### 删除一个tag标签

	git tag -d v3.0.0
	
### 删除远程tag标签

	git push origin --delete v3.0.0		

1. 创建分支
 	
 	创建分支很简单：git branch <分支名>
 	
2. 切换分支
 	
 	git checkout <分支名>
 该语句和上一个语句可以和起来用一个语句表示：git checkout -b <分支名>

3. 分支合并
	
	比如，如果要将开发中的分支（develop），合并到稳定分支（master），首先切换的master分支：git checkout master。然后执行合并操作：git merge develop。如果有冲突，会提示你，调用git status查看冲突文件。解决冲突，然后调用git add或git rm将解决后的文件暂存。所有冲突解决后，git commit 提交更改。

4. 分支衍合
	
	分支衍合和分支合并的差别在于，分支衍合不会保留合并的日志，不留痕迹，而 分支合并则会保留合并的日志。要将开发中的分支（develop），衍合到稳定分支（master）。首先切换的master分支：git checkout master。然后执行衍和操作：git rebase develop。如果有冲突，会提示你，调用git status查看冲突文件。解决冲突，然后调用git add或git rm将解决后的文件暂存。所有冲突解决后，git rebase --continue 提交更改。

5. 删除分支
     
     执行git branch -d <分支名>
     如果该分支没有合并到主分支会报错，可以用以下命令强制删除git branch -D <分支名>
