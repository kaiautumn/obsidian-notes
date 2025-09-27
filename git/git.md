备份、代码还原、协同开发、追溯代码的编写人和编写时间
最常用的版本控制器
>集中式版本控制工具 SVN、CVS
>分布式版本控制工具 Git
# Git常用命令
#### 基本配置
打开git bash
设置用户信息
>git config --global user.name "zhaiqiukai"
>git config --global user.email "19922044874@qq.com"

查看配置信息
>git config --global user.name
>git config --global user.email
#### 为常用指令配置别名（可选）
1. C:/Users/19220----->用户目录下创建.bashrc文件
或者
```git
touch ~/.bashrc
```
2. 在.bashrc文件中添加
```git
#用于输出git提交日志
alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
#用于输出当前目录所有文件及基本信息
alias ll='ls -al'
```
#### 获取本地仓库
任意位置创建空目录，此空目录就是我们的仓库
右键打开Git Bash
执行命令git init
>或者
>\$mkdir learngit，即创建一个空文件夹
>\$cd learngit
>\$pwd   --->显示当前目录
>git init
#### 基础指令
![[git工作原理.png]]
- alias git-log='git log --pretty=oneline --all --graph --abbrev-commit'
- **打开文件夹** cd\<文件夹名\>
- **查看所有文件** ll
- **创建新文件** touch test.txt
- **修改文件名** mv \<原文件名\> \<后文件名\>
- **删除某个文件** git rm\<文件名\>
- **查看文件修改详情** git diff \<文件名\>
- **添加文件至暂存区** git add \<filename\>
	git add. 将所有修改加入暂存区
- **将暂存区的修改撤掉** git reset HEAD \<文件名\>
- **暂存区->本地仓库** git commit
- **查看修改的状态** git status
- **提交暂存区到本地仓库** git commit -m"注释内容" 
- **vi编辑器：**
vi file.txt ( 可以Tab直接补全 )
>F12 insert
>输入编辑的内容
>esc 返回
>:wq 退出编辑器
> >然后这个文件就进入了工作区

- **git log 查看提交记录**
>cat  文件名  预览某个文件
>git log -all  显示所有分支
>git log --pretty=oneline  将提交的信息显示为一行
>git log --abbrev-commit 使输出的commitid更短
>git log ---graph   以图的形式显示
>git log --pretty=oneline --abbrev-commit 

- **版本回退**
 git reset --hard commitID
>- HEAD表示当前版本，HEAD^表示上个版本，HEAD^表示上上版本，HEAD~100表示100个版本以前。可以git reset --hard HEAD^
>- \-\-hard 表示回退到上个版本已提交状态，\-\-soft回退到上个版本未提交状态，\-\-mixed回退到上版本已添加但未提交的状态

- **看到已经删除的提交记录** git reflog
- **撤销修改，丢弃工作区的修改** git checkout --\<文件名\>，可以回退到最近一次git commit 或 git add的状态
- **删除文件**
>- rm <文件名>，将文件直接删除，但是会是的工作区和版本库不一致，status会告诉你哪2些文件被删除了
>- git rm 在版本库中删除文件，并且 git commit 

# 分支

 把工作从开发主线上分离出来进行重大bug修改以免影响主线
 在查看git-log时，HEAD->指针指向什么，就说明什么是当前分支
 在不同的分支内，会有不同的文件显示，但是git-log会显示所有的内容
 - 查看本地分支 git branch
 - 创建本地分支 git branch 分本地支名
 - 切换分支  git checkout 分支名
 - 修改分支名字 git branch -m <旧分支名字><新分支名字>
>还可以直接创建并切换一个新的分支 git checkout -b 分支名
>当然可以git switch 分支名
- 合并分支 git merge 分支名，本分支吸收另一个分支。合并的过程可以依据按图形显示日志
- 删除分支，只能删除其他分支，不能删除本分支 
>git branch -d 分支名，做各种检查后删除分支
>Git branch -D 分支名，不做任何检查，强制删除（比如一个分支未合并）
- 解决冲突，如两个分支同时修改了同一文件的同一行，两个分支分别进行add,commit后切换到master，后merge branch1branch2，就会报错。
[[分支冲突.png]] 
 此时就需要手动修改，点开发生冲突的文件（图中为file.txt）解决文件中的冲突部分后add加入暂存区，commit提交到仓库

---
#### 开发中分支的使用原则与流程
- master 分支
线上分支，主分支，中小规模项目作为线上运行的应用对应的分支
- develop分支
从master分支创建而来，一般作为开发部门的主要开发分支。最后合并到master分支上准备上线
- feature分支（新功能）
从develop创建的分支，一般是同期并行开发，但不同期上线时创建的分支，分支上的研发任务完成后合并到deelop分支
- hotfix分支
master分支创建而来，一般作为线上修bug使用，后合并到master、test、develop分支上
---
#### bug分支
突然遇到一个bug需要立即修复，但是你手上的工作还没做完。怎么办
git stash 可以把工作现场储存起来，修好后继续工作
在别的分支上修复bug，后提交，并删除修bug用到的分支
>git stash list 查看隐藏了什么东西
>git stash apply恢复，git stash drop删除
>git stash pop,恢复的同时也删除了

但是，主分支上存在的bug你的分支也可能有，可以使用
git cherry-pick\<commit\>直接把修改“复制”到当前分支，避免重复劳动
#### Feature分支
没添加一个新功能，最好新建一个feature分支，在上面开发然后合并，最后删除feature分支
如果要弄丢一个没有合并的分支，可以通过git branch -D\<name\>

# 远程仓库
#### 基础指令
常用的远程仓库有github、码云、Gitlab等
码云服务器速度更快，和github都是开源的
GItlab是隐藏的
> **构建云仓库**
>git bash
>**创建SSH Key** $ssh-keygen -t rsa -C "1922044874\@qq.com"
>一路回车，然后在目录里找到.ssh目录，id_rsa时私钥，id_rsa.pug是公钥
>在github settings里找到SSH页面，Add SSH Key，填上title，Key 文本框粘贴id_rsa.pub
>然后github创建一个新的仓库
>
>**云端仓库与本地仓库建立联系**
>git remote add /<远端名称/>/<仓库路径/>
>>远端名称默认是origin，取决于远端服务器设置，仓库路径从远端服务器获取URL
>>git remote add origin git\@github.com:autumn/learngit.git
>
>git remote 查看远程仓库名称
>git remote set-url origin <新仓库地址> 修改远程仓库的地址
>
> **提交文件**
>>git push origin master 推送到远程仓库，这里的origin是远程仓库的名称
>>git push\[-f\]\[--set-upstream\]\[远端名\]\[本地分支名\]\[:要push到的远端分支名\]
>>git push --set-upstream origin master 推送到远端时建立起和远端分支的关系
>>当前分支和远端分支已有联系，则可以省略分支名和远端名,git push
>
>git branch -vv 查看本地和远端的分支对应关系
>
>###### 删除远程库
>先git remote -v查看远程库信息
>git remote rm\<name\>，name为在git bash上-v后显示的远程仓库的名字

#### 克隆
**从远端云端弄到本地仓库** 
git clone\<仓库路径\>\<本地目录\>
>git clone git\@github.com:kaiautumn/learngit.git

>[!warning]
>**尝试克隆的时候应该在桌面上打开bash，然后克隆**

#### 抓取和拉取
 - 抓取
 git fetch \<remote name/origin\>\<branch name\>
 抓取指令就是仓库里的更新都抓取到本地，不进行合并
 - 拉取
 git pull \<remote name/origin\>\<branch name\>
 拉取指令就是将远端仓库修改拉到本地并自动合并，等同于fetch+merge

# 标签管理
标签实际上就是指向某个commit的指针
切换到要打标签的分支上
>**打标签** git tag \<name\>
>**查看所有标签** git tag
>- 有时候忘了打标签
>>git-log找到忘记的commit后记住commitID
>>git tag <\name> <\commitID>
>
>**查看标签信息**git show <\tagname>
>**删除标签** git tag -d <\tagname>

# 忽略特殊文件
>创建一个.gitignore文件，列出要忽视的文件模式
>- no .a files
>\*.a
>- but do track lib.a , even though you are ignoring .a files above
>!lib .a 
>- only ignore the TODO file in the current directory, not subdir/TODO
>/TODO
>- ignore all files in the build/ directory
>build/
>- ignore doc/notes.txt, but not doc/server/arch.txt
>doc/\*.txt
>- ignore all .pdf files in the doc/directory
>doc\/\*\*\/\*\.pdf

---

>[!note]
>在github上新建一个库，在本地桌面克隆，进入本地文件夹，然后即可修改
