# git版本控制

## github

### 安装git

进入git官网[下载](https://git-scm.com/downloads)页面，下载适配操作系统的安装包，进行安装

### git配置

```
git config -e    # 针对当前仓库 
git config --list  #查看git配置
git config --global user.name "wanghua"
git config --global user.email test@runoob.com

#只对当前仓库有效
git config user.name "wanghua"
git config user.email test@runoob.com
```


### 创建仓库

* 网页创建

#### 1.登录[github](www.github.com)

#### 2.创建新的仓库

#### 3.克隆到本地：

```
git clone git@github.com:***/test.git test_1
```

#### 4.编辑文件

#### 5.上传更新到github

```
git status ##查看git状态
git add . ##将本目录下所有文件加入到index
git commit -m "comment" ##将版本加入到HEAD
git push -u origin master:test ##origin指的是关联的远程仓库，master指的是本地分支，test指的是远程分支，注意本地分支应该先创建,-u在下次仓库不再是空的时候可以去除
```

#### 6.到github所在仓库的分支下请求合并“Pull request”

* 本地创建

#### 1.指定仓库目录

#### 2.初始化

```
git init
```

#### 3.编辑仓库

#### 4.加入到HEAD

```
git add .
git commit -m "comment" ##将版本加入到HEAD
```

由于本地Git仓库和Github仓库之间的传输是通过SSH加密的，所以连接时需要设置一下：

#### 5.创建SSH KEY

```
~/.ssh ##检查之前是否生成了KEY
ssh-keygen -t rsa -C "email"  #一直enter，不要设置密码
ssh -T git@github.com
cat ~/.ssh/id_rsa.pub
```

打开github账户的设置，进入"SSH and GPG keys"，新建，输入id和上个命令输出的秘钥

#### 6.在github上新建仓库

#### 7.创建本地仓库与远程仓库的连接

```
git remote add origin 远程仓库
```

#### 8.更新远程仓库

```
git push -u origin master:test
```

### 拉取仓库

#### 1.创建和更改本地与远程的连接

```
git remote add origin 远程仓库


git remote rm origin
git remote add origin 远程仓库
```

#### 2.从远程获取代码并合并本地的版本

```
git pull <远程主机名> <远程分支名>:<本地分支名>
git pull origin master:brantest
```

### 分支管理

#### 1.创建分支

```
git branch <branch name>
git checkout -b <branch name>
```

#### 2.版本控制

```
1.通过提交记录来进行版本控制
git log
git reflog
2.通过分支控制版本，但是需要注意的是修改后需要commit后再切换回你想要去的分支，这样原分支的更改将不会被更新到其他分支，否则工作区的修改将是全局修改，因此核心仍旧是提交记录来进行修改
```

#### 3.合并分支

```
git checkout master
git merge develop
```

#### 4.版本回退

```
撤销修改
	1、只在工作区修改了,没提交到暂存区 
		git checkout -- index.html 撤销工作区修改
			其实 git checkout -- file 就是用暂存区的版本来代替工作区的版本
	
	2、修改提交到暂存区之后(即git add 后,git commit 之前)
		先使用$ git reset HEAD index.html 将暂存区的修改撤销掉，重新放回工作区，
		git checkout -- index.html 撤销工作区修改
		
	3、已经提交到本地的版本库分支master上了(前提是没推送到远程版本库,git commit 后,git push 之前)
		git reset --hard commitId		版本回退

```

#### 5.删除分支

```
删除分支
	1、删除本地分支
		git branch -d 分支名
	
	2、删除仓库远程分支
		git push origin --delete 分支名
	
	3、批量删除本地分支
		git branch |xargs git branch -D 强制删除所有分支
		git branch |xargs git branch -d 删除本地所有与远程仓库同步分支（本地修改过未提交的不会删除）
		git branch |grep "xxbranch"|xargs git branch -d 删除本地部分grep匹配的分支
```

注意：新建空的文件夹并不会认为是更改

#### 6.标签管理

```
$ git tag -a v1.0 
```

### 版本控制

```
1.通过提交记录来进行版本控制
git log
git reflog
2.通过分支控制版本，但是需要注意的是修改后需要commit后再切换回你想要去的分支，这样原分支的更改将不会被更新到其他分支，否则工作区的修改将是全局修改，因此核心仍旧是提交记录来进行修改
```

## gitee

```
和github大同小异，关键在于
```

