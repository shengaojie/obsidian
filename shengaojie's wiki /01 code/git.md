
> [!compare] 集中式版本控制  VS 分布式版本控制
> * 最常见的集中式版本控制系统是SVN，版本库是集中放在中央处理器中的，而干活的时候，用的都是自己电脑，所以首先要从中央服务器那里得到最新的版本，然后开始干活，干完活后，需要把自己做完的活推送到中央服务器。而且集中式版本控制系统是必须联网才能工作的，一旦断网，所有人都干不成活了，可想而知，集中式版本控制系统的局限性有多大。
> * Git是目前世界上最流行的分布式版本控制系统，它没有中央处理器，每个人的电脑就是一个完整的版本库，这样，工作的时候就不需要联网了，因为版本都是在自己的电脑上，随时都可以将自己在工作区间做的修改提交到本地仓库，最后将自己的本地版本仓库推动到远程版本仓库进行合并，效率可想而知是可控的贼高。



> [!compare] 工作区、暂存区、版本库
> 工作区：就是你电脑中看到一般目录  
> 暂存区：一般在`.git`目录下的`index`文件中，所以有的时候的暂存区也叫索引  
> 版本库：本地仓库，`.git`文件就是本地版本仓库

![[CleanShot 2024-01-14 at 14.05.52@2x.png]]
* 左侧是工作区，右侧为版本库。在版本库中的`index`的区域就是暂存区，master表示的是当前的分支
* `HEAD`实际上是指向分支的一个游标，当前指向的是master
* 图中的`objects` 表示的区域为Git的对象库，位于`.git/objects`目录下，里面包含了创建的各种对象和内容
* 可以简单理解为，需要提交的文件都是先放在暂存区的，让后通过`git commit`一次性提交暂存区的所有的修改



# 命令
```shell   
git init
git status
git add
git commit -m "info"
git commit -a -m "info"

git branch newBranch
git checkout newBranch
git merge newBranch
git reset --hard 版本号
git restore a.txt
```


> [!NOTE] 创建版本库
> 1. 从终端进入到一个项目目录下
> 2. 使用`git init`将这个目录变成git可以管理的仓库
> 此时当前的文件夹下会多出一个`.git`目录，需要通过`ll -ah`来查看


> [!NOTE] 添加文件到版本库

1. 先在当前目录下创建一个文件`a.txt`
```shell
touch a.txt
```

2. 通过`git add`提交到暂存区
	1. 使用`git status` 命令可以查看此时的状态信息
		![[CleanShot 2024-01-14 at 14.16.58@2x.png|525]]
  提示信息告诉我们，在main分之上，有一个未被追踪到的文件`a.txt`,我们需要先通过`git add` 先add到暂存区中
	2.  使用`git add`,提交到暂存区中
	3.  再次使用`git status`查看此时的状态
		![[CleanShot 2024-01-14 at 14.24.09@2x.png]]
		告诉我们此时需要将暂存区中的文件提交到本地缓存中

3. 使用git commit 命令提交到本地仓库中
```shell
git commit -m "add a.txt"
```
最后在通过`git status`查看此时的状态
![[CleanShot 2024-01-14 at 14.27.52@2x.png|500]]




> [!NOTE] 版本回退
> 1. `git log`查看所有的提交记录，可以使用`git log --oneline`来简化显示信息
> 	![[CleanShot 2024-01-14 at 14.42.37@2x.png]]
> 	可以看到此时有两个版本
> 2. `git reset --hard 版本号`，使用  
> `git reset --hard 7faede6`,回到`add a.txt`这个版本




> [!principle] git撤销修改

> [!NOTE] git撤销工作区的修改
1. 我们修改一下`a.txt`文件，并且通过`git status`查看此时的状态
	![[CleanShot 2024-01-14 at 14.53.38@2x.png]]
	告诉我们可以通过`git add`加入到暂存区中，或者是通过`git restore file`撤回
 2. `git restore a.txt`


> [!NOTE] 撤销暂存区的修改
> `git restore --staged readme.txt `   从暂存区撤回，退回到工作区状态





> [!NOTE] 分支相关的操作
> 1. `git branch b1`      # 创建新的分支
> 2. `git checkout b1`     # 切换到分支
> 3. `git checkout master   git merge b1`    # 切换分支到master，合并b1分支
合并分支的时候可能会发生冲突。需要手动的选择，然后在将该文件通过`git add`和`git commit`提交上去







