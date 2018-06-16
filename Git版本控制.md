
#### 第一章：课程路线图

##### 第1节：如何学习Gitbeijing?
```
 1.大系统、细节多，不需面面俱到学习
 2.官方文档：Documentation (https://git-scm.com/doc) ，有点深，初学者不推荐学习
 3.推荐配合  GitHub网站去学习；职业开发者使用的网站，或英文不好请参考：CODING中文网站
```
##### 第2节.在Windows上安装Git
```
1、官网下载网址：https://git-scm.com/downloads
2、打开网页后选择选择Windows下载
3、下载完成后，然后按默认选项安装即可。
4、安装完成后，在开始菜单里找到“Git”->“Git Bash”，蹦出一个类似命令行窗口的东西，就说明Git安装成功！
5、安装完成后，还需要最后一步设置，在命令行输入：
$ git config --global user.name "Your Name"
$ git config --global user.email "email@example.com"
6、因为Git是分布式版本控制系统，所以，每个机器都必须自报家门：你的名字和Email地址。你也许会担心，
如果有人故意冒充别人怎么办？这个不必担心，首先我们相信大家都是善良无知的群众，其次，真的有冒充的也是有办法可查的。
7、注意git config命令的--global参数，用了这个参数，表示你这台机器上所有的Git仓库都会使用这个配置，
当然也可以对某个仓库指定不同的用户名和Email地址。
```
##### 第3节.创建版本库
```
版本库又名仓库，英文名repository，你可以简单理解成一个目录，这个目录里面的所有文件都可以被Git管理起来，
每个文件的修改、删除，Git都能跟踪，以便任何时刻都可以追踪历史，或者在将来某个时刻可以“还原”。
所以，创建一个版本库非常简单，首先，选择一个合适的地方，
```
###### 第一步，创建一个空目录：
```
$ mkdir learngit
$ cd learngit
$ pwd
/Users/michael/learngit
pwd命令用于显示当前目录。在Mac上，这个仓库位于/Users/michael/learngit。
如果使用Windows系统，为了避免遇到各种莫名其妙的问题，请确保目录名（包括父目录）不包含中文。
```
###### 第二步，通过git init命令把这个目录变成Git可以管理的仓库：
```
$ git init
Initialized empty Git repository in /Users/michael/learngit/.git/
瞬间Git就把仓库建好了，而且告诉你是一个空的仓库（empty Git repository），
细心的读者可以发现当前目录下多了一个.git的目录，这个目录是Git来跟踪管理版本库的，
没事千万不要手动修改这个目录里面的文件，不然改乱了，就把Git仓库给破坏了。

如果你没有看到.git目录，那是因为这个目录默认是隐藏的，用ls -ah命令就可以看见。

也不一定必须在空目录下创建Git仓库，选择一个已经有东西的目录也是可以的。不过，
不建议你使用自己正在开发的公司项目来学习Git，否则造成的一切后果概不负责。

把文件添加到版本库
首先这里再明确一下，所有的版本控制系统，其实只能跟踪文本文件的改动，比如TXT文件，网页，所有的程序代码等等，
Git也不例外。版本控制系统可以告诉你每次的改动，比如在第5行加了一个单词“Linux”，在第8行删了一个单词“Windows”。
而图片、视频这些二进制文件，虽然也能由版本控制系统管理，但没法跟踪文件的变化，只能把二进制文件每次改动串起来，
也就是只知道图片从100KB改成了120KB，但到底改了啥，版本控制系统不知道，也没法知道。

不幸的是，Microsoft的Word格式是二进制格式，因此，版本控制系统是没法跟踪 Word 文件的改动的，
前面我们举的例子只是为了演示，如果要真正使用版本控制系统，就要以纯文本方式编写文件。

因为文本是有编码的，比如中文有常用的GBK编码，日文有 Shift_JIS 编码，如果没有历史遗留问题，
强烈建议使用标准的UTF-8编码，所有语言使用同一种编码，既没有冲突，又被所有平台所支持。

使用Windows要特别注意：

千万不要使用Windows自带的记事本编辑任何文本文件。原因是Microsoft开发记事本的团队使用了一个非常弱智的行为来
保存UTF-8编码的文件，他们自作聪明地在每个文件开头添加了0xefbbbf（十六进制）的字符，你会遇到很多不可思议的问题，
比如，网页第一行可能会显示一个“?”，明明正确的程序一编译就报语法错误，等等，都是由记事本的弱智行为带来的。
建议你下载 **Notepad++** 代替记事本，不但功能强大，记得把 Notepad++ 的默认编码设置为 UTF-8 without BOM 即可：

set-utf8-notepad++
```
###### 第三步，我们编写一个readme.txt文件
```
内容如下：
Git is a version control system.
Git is free software.
一定要放到learngit目录下（子目录也行），因为这是一个 Git仓库，放到其他地方Git再厉害也找不到这个文件。

和把大象放到冰箱需要3步相比，把一个文件放到Git仓库只需要两步。

第一步，用命令 git add 告诉Git，把文件添加到仓库：
$ git add readme.txt
执行上面的命令，没有任何显示，这就对了，Unix 的哲学是“没有消息就是好消息”，说明添加成功。

第二步，用命令 git commit 告诉 Git，把文件提交到仓库：
$ git commit -m "wrote a readme file"
[master (root-commit) cb926e7] wrote a readme file
 1 file changed, 2 insertions(+)
 create mode 100644 readme.txt
简单解释一下git commi t命令，-m后面输入的是本次提交的说明，可以输入任意内容，当然最好是有意义的，
这样你就能从历史记录里方便地找到改动记录。

嫌麻烦不想输入-m "xxx"行不行？确实有办法可以这么干，但是强烈不建议你这么干，因为输入说明对自己对别人阅读都很重要。
实在不想输入说明的童鞋请自行Google，我不告诉你这个参数。

git commit命令执行成功后会告诉你，1个文件被改动（我们新添加的readme.txt文件），插入了两行内容（readme.txt有两行内容）。

为什么Git添加文件需要add，commit一共两步呢？因为commit可以一次提交很多文件，所以你可以多次add不同的文件，比如：

$ git add file1.txt
$ git add file2.txt file3.txt
$ git commit -m "add 3 files."
```
###### 现在总结一下今天学的两点内容：
```
初始化一个Git仓库，使用git init命令。
添加文件到Git仓库，分两步：
第一步，使用命令git add <file>，注意，可反复多次使用，添加多个文件；
第二步，使用命令git commit，完成。
```
##### 第二章.时光机穿梭
###### 第一节 版本查看及状态查询
###### 修改文件
```
成功地添加并提交了一个readme.txt文件，我们继续修改readme.txt文件，改成如下内容：

Git is a distributed version control system.
Git is free software.
```
###### git status命令查看状态
```
现在，运行git status命令看看结果：

$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#    modified:   readme.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
git status命令可以让我们时刻掌握仓库当前的状态，上面的命令告诉我们，readme.txt被修改过了，但还没有准备提交的修改。
```
###### git diff命令查看修改差异
```
虽然Git告诉我们readme.txt被修改了，但如果能看看具体修改了什么内容，自然是很好的。比如你休假两周从国外回来，第一天上班时，
已经记不清上次怎么修改的readme.txt，所以，需要用git diff这个命令看看：

$ git diff readme.txt 
diff --git a/readme.txt b/readme.txt
index 46d49bf..9247db6 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,2 +1,2 @@
-Git is a version control system.
+Git is a distributed version control system.
 Git is free software.
git diff顾名思义就是查看difference，显示的格式正是Unix通用的diff格式，可以从上面的命令输出看到，
我们在第一行添加了一个“distributed”单词。
```
###### git add 命令添加
```
知道了对readme.txt作了什么修改后，再把它提交到仓库就放心多了，提交修改和提交新文件是一样的两步，第一步是git add：

$ git add readme.txt
同样没有任何输出。在执行第二步git commit之前，我们再运行git status看看当前仓库的状态：

$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       modified:   readme.txt
#
 ```
###### git commit 命令提交
```
git status告诉我们，将要被提交的修改包括readme.txt，下一步，就可以放心地提交了：

$ git commit -m "add distributed"
[master ea34578] add distributed
 1 file changed, 1 insertion(+), 1 deletion(-)
 ###### git status命令再次查看提交的状态
提交后，我们再用git status命令看看仓库的当前状态：

$ git status
# On branch master
nothing to commit (working directory clean)
Git告诉我们当前没有需要提交的修改，而且，工作目录是干净（working directory clean）的。

小结
要随时掌握工作区的状态，使用git status命令。

如果git status告诉你有文件被修改过，用git diff可以查看修改内容。
```
##### 第二节：版本回退
###### 再修改readme.txt文件
```
如下：
Git is a distributed version control system.
Git is free software distributed under the GPL.
然后尝试提交：

$ git add readme.txt
$ git commit -m "append GPL"
[master 3628164] append GPL
 1 file changed, 1 insertion(+), 1 deletion(-)
像这样，你不断对文件进行修改，然后不断提交修改到版本库里，就好比玩RPG游戏时，每通过一关就会自动把游戏状态存盘，
如果某一关没过去，你还可以选择读取前一关的状态。有些时候，在打Boss之前，你会手动存盘，以便万一打Boss失败了，
可以从最近的地方重新开始。Git也是一样，每当你觉得文件修改到一定程度的时候，就可以“保存一个快照”，这个快照在
Git中被称为commit。一旦你把文件改乱了，或者误删了文件，还可以从最近的一个commit恢复，然后继续工作，而不是把
几个月的工作成果全部丢失。

现在，我们回顾一下readme.txt文件一共有几个版本被提交到Git仓库里了：

版本1：wrote a readme file

Git is a version control system.
Git is free software.
版本2：add distributed

Git is a distributed version control system.
Git is free software.
版本3：append GPL

Git is a distributed version control system.
Git is free software distributed under the GPL.
```
###### git log命令查看版本
```
当然了，在实际工作中，我们脑子里怎么可能记得一个几千行的文件每次都改了什么内容，不然要版本控制系统干什么。
版本控制系统肯定有某个命令可以告诉我们历史记录，在Git中，我们用git log命令查看：

$ git log
commit 3628164fb26d48395383f8f31179f24e0882e1e0
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 15:11:49 2013 +0800

    append GPL

commit ea34578d5496d7dd233c827ed32a8cd576c5ee85
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 14:53:12 2013 +0800

    add distributed

commit cb926e7ea50ad11b8f9e909c05226233bf755030
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Mon Aug 19 17:51:55 2013 +0800

    wrote a readme file
```
###### 加上--pretty=oneline参数只查看所有版本
```
git log命令显示从最近到最远的提交日志，我们可以看到3次提交，最近的一次是append GPL，上一次是add distributed，
最早的一次是wrote a readme file。
如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数：

$ git log --pretty=oneline
3628164fb26d48395383f8f31179f24e0882e1e0 append GPL
ea34578d5496d7dd233c827ed32a8cd576c5ee85 add distributed
cb926e7ea50ad11b8f9e909c05226233bf755030 wrote a readme file
需要友情提示的是，你看到的一大串类似3628164...882e1e0的是commit id（版本号），和SVN不一样，Git的commit id不是
1，2，3……递增的数字，而是一个SHA1计算出来的一个非常大的数字，用十六进制表示，而且你看到的commit id和我的肯定
不一样，以你自己的为准。为什么commit id需要用这么一大串数字表示呢？因为Git是分布式的版本控制系统，后面我们还要
研究多人在同一个版本库里工作，如果大家都用1，2，3……作为版本号，那肯定就冲突了。

每提交一个新版本，实际上Git就会把它们自动串成一条时间线。如果使用可视化工具查看Git历史，就可以更清楚地看到提交历史的时间线：

git-log-timeline

好了，现在我们启动时光穿梭机，准备把readme.txt回退到上一个版本，也就是“add distributed”的那个版本，怎么做呢？

首先，Git必须知道当前版本是哪个版本，在Git中，用HEAD表示当前版本，也就是最新的提交3628164...882e1e0
（注意我的提交ID和你的肯定不一样），上一个版本就是HEAD^，上上一个版本就是HEAD^^，当然往上100个版本写
100个^比较容易数不过来，所以写成HEAD~100。
```
###### git reset命令回退到上一个版本
```
现在，我们要把当前版本“append GPL”回退到上一个版本“add distributed”，就可以使用git reset命令：

$ git reset --hard HEAD^
HEAD is now at ea34578 add distributed
--hard参数有啥意义？这个后面再讲，现在你先放心使用。

看看readme.txt的内容是不是版本add distributed：

$ cat readme.txt
Git is a distributed version control system.
Git is free software.
果然。

还可以继续回退到上一个版本wrote a readme file，不过且慢，然我们用git log再看看现在版本库的状态：

$ git log
commit ea34578d5496d7dd233c827ed32a8cd576c5ee85
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Tue Aug 20 14:53:12 2013 +0800

    add distributed

commit cb926e7ea50ad11b8f9e909c05226233bf755030
Author: Michael Liao <askxuefeng@gmail.com>
Date:   Mon Aug 19 17:51:55 2013 +0800

    wrote a readme file
最新的那个版本append GPL已经看不到了！好比你从21世纪坐时光穿梭机来到了19世纪，想再回去已经回不去了，肿么办？
```
###### git reset --hard 3628164加上了版本号直接搜索到对应的内容
```
办法其实还是有的，只要上面的命令行窗口还没有被关掉，你就可以顺着往上找啊找啊，找到那个append GPL的commit id是
3628164...，于是就可以指定回到未来的某个版本：

$ git reset --hard 3628164
HEAD is now at 3628164 append GPL
版本号没必要写全，前几位就可以了，Git会自动去找。当然也不能只写前一两位，因为Git可能会找到多个版本号，
就无法确定是哪一个了。

再小心翼翼地看看readme.txt的内容：

$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
果然，我胡汉三又回来了。

Git的版本回退速度非常快，因为Git在内部有个指向当前版本的HEAD指针，当你回退版本的时候，Git仅仅是把HEAD从指向append GPL：

git-head

改为指向add distributed：

git-head-move

然后顺便把工作区的文件更新了。所以你让HEAD指向哪个版本号，你就把当前版本定位在哪。

 现在，你回退到了某个版本，关掉了电脑，第二天早上就后悔了，想恢复到新版本怎么办？找不到新版本的commit id怎么办？
```
###### ggit reflog查看命令历史
```
在Git中，总是有后悔药可以吃的。当你用$ git reset --hard HEAD^回退到add distributed版本时，再想恢复到append GPL，
就必须找到append GPL的commit id。Git提供了一个命令git reflog用来记录你的每一次命令：

$ git reflog
ea34578 HEAD@{0}: reset: moving to HEAD^
3628164 HEAD@{1}: commit: append GPL
ea34578 HEAD@{2}: commit: add distributed
cb926e7 HEAD@{3}: commit (initial): wrote a readme file
终于舒了口气，第二行显示append GPL的commit id是3628164，现在，你又可以乘坐时光机回到未来了。

小结
现在总结一下：

HEAD指向的版本就是当前版本，因此，Git允许我们在版本的历史之间穿梭，使用命令git reset --hard commit_id。

穿梭前，用git log可以查看提交历史，以便确定要回退到哪个版本。

要重返未来，用git reflog查看命令历史，以便确定要回到未来的哪个版本。
```
##### 第三节：工作区和暂存区
```
Git和其他版本控制系统如SVN的一个不同之处就是有暂存区的概念。
```
###### 工作区和暂存区的概念
```
工作区（Working Directory）
就是你在电脑里能看到的目录，比如我的learngit文件夹就是一个工作区：

working-dir

版本库（Repository）
工作区有一个隐藏目录.git，这个不算工作区，而是Git的版本库。

Git的版本库里存了很多东西，其中最重要的就是称为stage（或者叫index）的暂存区，还有Git为我们自动创建的第一个
分支master，以及指向master的一个指针叫HEAD。

git-repo

分支和HEAD的概念我们以后再讲。

前面讲了我们把文件往Git版本库里添加的时候，是分两步执行的：
```
###### 第一步是用git add把文件添加进去，实际上就是把文件修改添加到暂存区；

###### 第二步是用git commit提交更改，实际上就是把暂存区的所有内容提交到当前分支。
```
因为我们创建Git版本库时，Git自动为我们创建了唯一一个master分支，所以，现在，git commit就是往master分支上提交更改。

你可以简单理解为，需要提交的文件修改通通放到暂存区，然后，一次性提交暂存区的所有修改。

俗话说，实践出真知。现在，我们再练习一遍，先对readme.txt做个修改，比如加上一行内容：

Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
然后，在工作区新增一个LICENSE文本文件（内容随便写）。

先用git status查看一下状态：

$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   readme.txt
#
# Untracked files:
#   (use "git add <file>..." to include in what will be committed)
#
#       LICENSE
no changes added to commit (use "git add" and/or "git commit -a")
Git非常清楚地告诉我们，readme.txt被修改了，而LICENSE还从来没有被添加过，所以它的状态是Untracked。

现在，使用两次命令git add，把readme.txt和LICENSE都添加后，用git status再查看一下：

$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       new file:   LICENSE
#       modified:   readme.txt
#
现在，暂存区的状态就变成这样了：

git-stage

所以，git add命令实际上就是把要提交的所有修改放到暂存区（Stage），然后，
执行git commit就可以一次性把暂存区的所有修改提交到分支。

$ git commit -m "understand how stage works"
[master 27c9860] understand how stage works
 2 files changed, 675 insertions(+)
 create mode 100644 LICENSE
一旦提交后，如果你又没有对工作区做任何修改，那么工作区就是“干净”的：

$ git status
# On branch master
nothing to commit (working directory clean)
现在版本库变成了这样，暂存区就没有任何内容了：

git-stage-after-commit

小结
暂存区是Git非常重要的概念，弄明白了暂存区，就弄明白了Git的很多操作到底干了什么。

没弄明白暂存区是怎么回事的童鞋，请向上滚动页面，再看一次。
```
##### 第四节：管理修改
```
现在，假定你已经完全掌握了暂存区的概念。下面，我们要讨论的就是，为什么Git比其他版本控制系统设计得优秀，
因为Git跟踪并管理的是修改，而非文件。

你会问，什么是修改？比如你新增了一行，这就是一个修改，删除了一行，也是一个修改，更改了某些字符，也是一个修改，
删了一些又加了一些，也是一个修改，甚至创建一个新文件，也算一个修改。

为什么说Git管理的是修改，而不是文件呢？我们还是做实验。第一步，对readme.txt做一个修改，比如加一行内容：

$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes.
然后，添加：

$ git add readme.txt
$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       modified:   readme.txt
#
然后，再修改readme.txt：

$ cat readme.txt 
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
提交：

$ git commit -m "git tracks changes"
[master d4f25b6] git tracks changes
 1 file changed, 1 insertion(+)
提交后，再看看状态：

$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   readme.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
咦，怎么第二次的修改没有被提交？

别激动，我们回顾一下操作过程：
```
###### 第一次修改 -> git add -> 第二次修改 -> git commit
```
你看，我们前面讲了，Git管理的是修改，当你用git add命令后，在工作区的第一次修改被放入暂存区，准备提交，但是，
在工作区的第二次修改并没有放入暂存区，所以，git commit只负责把暂存区的修改提交了，也就是第一次的修改被提交了，
第二次的修改不会被提交。

提交后，用git diff HEAD -- readme.txt命令可以查看工作区和版本库里面最新版本的区别：

$ git diff HEAD -- readme.txt 
diff --git a/readme.txt b/readme.txt
index 76d770f..a9c5755 100644
--- a/readme.txt
+++ b/readme.txt
@@ -1,4 +1,4 @@
 Git is a distributed version control system.
 Git is free software distributed under the GPL.
 Git has a mutable index called stage.
-Git tracks changes.
+Git tracks changes of files.
可见，第二次修改确实没有被提交。

 那怎么提交第二次修改呢？你可以继续git add再git commit，也可以别着急提交第一次修改，
 ```
###### 先git add第二次修改，再git commit，就相当于把两次修改合并后一块提交了

###### 第一次修改 -> git add -> 第二次修改 -> git add -> git commit
```
好，现在，把第二次修改提交了，然后开始小结。

小结
现在，你又理解了Git是如何跟踪修改的，每次修改，如果不add到暂存区，那就不会加入到commit中。
```
##### 第五节：撤销修改
```
自然，你是不会犯错的。不过现在是凌晨两点，你正在赶一份工作报告，你在readme.txt中添加了一行：

$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
My stupid boss still prefers SVN.
在你准备提交前，一杯咖啡起了作用，你猛然发现了“stupid boss”可能会让你丢掉这个月的奖金！

既然错误发现得很及时，就可以很容易地纠正它。你可以删掉最后一行，手动把文件恢复到上一个版本的状态。
如果用git status查看一下：

$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   readme.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
你可以发现，Git会告诉你，git checkout -- file可以丢弃工作区的修改：

$ git checkout -- readme.txt
命令git checkout -- readme.txt意思就是，把readme.txt文件在工作区的修改全部撤销，这里有两种情况：

一种是readme.txt自修改后还没有被放到暂存区，现在，撤销修改就回到和版本库一模一样的状态；

一种是readme.txt已经添加到暂存区后，又作了修改，现在，撤销修改就回到添加到暂存区后的状态。

总之，就是让这个文件回到最近一次git commit或git add时的状态。

现在，看看readme.txt的文件内容：

$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
文件内容果然复原了。
```
###### git checkout -- file命令中的--很重要，没有--，就变成了“切换到另一个分支”的命令，我们在后面的分支管理中会再次遇到git checkout命令。
```
 现在假定是凌晨3点，你不但写了一些胡话，还git add到暂存区了：

$ cat readme.txt
Git is a distributed version control system.
Git is free software distributed under the GPL.
Git has a mutable index called stage.
Git tracks changes of files.
My stupid boss still prefers SVN.

$ git add readme.txt
庆幸的是，在commit之前，你发现了这个问题。用git status查看一下，修改只是添加到了暂存区，还没有提交：

$ git status
# On branch master
# Changes to be committed:
#   (use "git reset HEAD <file>..." to unstage)
#
#       modified:   readme.txt
#
Git同样告诉我们，用命令git reset HEAD file可以把暂存区的修改撤销掉（unstage），重新放回工作区：

$ git reset HEAD readme.txt
Unstaged changes after reset:
M       readme.txt
```
###### git reset命令既可以回退版本，也可以把暂存区的修改回退到工作区。当我们用HEAD时，表示最新的版本。
```
再用git status查看一下，现在暂存区是干净的，工作区有修改：

$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       modified:   readme.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
还记得如何丢弃工作区的修改吗？

$ git checkout -- readme.txt

$ git status
# On branch master
nothing to commit (working directory clean)
整个世界终于清静了！

 现在，假设你不但改错了东西，还从暂存区提交到了版本库，怎么办呢？还记得版本回退一节吗？可以回退到上一个版本。不过，
 这是有条件的，就是你还没有把自己的本地版本库推送到远程。还记得Git是分布式版本控制系统吗？我们后面会讲到远程版本库，
 一旦你把“stupid boss”提交推送到远程版本库，你就真的惨了……

小结
又到了小结时间。
```
###### 场景1：当你改乱了工作区某个文件的内容，想直接丢弃工作区的修改时，用命令git checkout -- file。

###### 场景2：当你不但改乱了工作区某个文件的内容，还添加到了暂存区时，想丢弃修改，分两步，第一步用命令
git reset HEAD file，就回到了场景1，第二步按场景1操作。

###### 场景3：已经提交了不合适的修改到版本库时，想要撤销本次提交，参考版本回退一节，不过前提是没有推送到远程库。

##### 第六节：删除文件
```
在Git中，删除也是一个修改操作，我们实战一下，先添加一个新文件test.txt到Git并且提交：

$ git add test.txt
$ git commit -m "add test.txt"
[master 94cdc44] add test.txt
 1 file changed, 1 insertion(+)
 create mode 100644 test.txt
一般情况下，你通常直接在文件管理器中把没用的文件删了，或者用rm命令删了：

$ rm test.txt
这个时候，Git知道你删除了文件，因此，工作区和版本库就不一致了，git status命令会立刻告诉你哪些文件被删除了：

$ git status
# On branch master
# Changes not staged for commit:
#   (use "git add/rm <file>..." to update what will be committed)
#   (use "git checkout -- <file>..." to discard changes in working directory)
#
#       deleted:    test.txt
#
no changes added to commit (use "git add" and/or "git commit -a")
现在你有两个选择，一是
```
###### 确实要从版本库中删除该文件，那就用命令git rm删掉，并且git commit：
```
$ git rm test.txt
rm 'test.txt'
$ git commit -m "remove test.txt"
[master d17efd8] remove test.txt
 1 file changed, 1 deletion(-)
 delete mode 100644 test.txt
现在，文件就从版本库中被删除了。

另一种情况是删错了，因为版本库里还有呢，所以可以很轻松地把误删的文件恢复到最新版本：

$ git checkout -- test.txt
```
###### git checkout其实是用版本库里的版本替换工作区的版本，无论工作区是修改还是删除，都可以“一键还原”。
```
小结
命令git rm用于删除一个文件。如果一个文件已经被提交到版本库，那么你永远不用担心误删，但是要小心，
你只能恢复文件到最新版本，你会丢失最近一次提交后你修改的内容。

```
#### 第二章：搬进Github

##### 第1节：本章介绍
```
 Github 真的让日常版本控制工作变得简单，
 老师Peter 的 Github 账号 在（http://github.com/happypeter）
 Git 和 Github 是两个东西
 Git 是一个本地的版本控制工具，Github 是项目托管工具；Github 让Git 变得更易用
```
##### 第2节：浏览器中使用 github
```
注册并使用 github.com 。不会用 git ，就不能用 github 吗? 不是这样的。
Github 的网站上通过网页操作就已经能实现很多强大的版本控制功能了.

注册地址： http://github.com 
填写自己的用户名邮箱、密码，点击 Sign up for Github 按钮。对于开源项目 github 是免费的，所以不用管付费相关的内容。
接下来初次注册的用户会看到一共四步的 github 使用教程。
另外你可能还会看到要求新用户去验证一下邮箱地址的提示，到邮箱之中找到验证邮件，点一下里面的链接就可以了。

一个项目其实就是一个文件夹，里面放着所有的项目文件，可以是代码，也可以是任意的文档。但是在 github 这里，
每一个项目都不仅仅是最新版本的代码，还保持着所有的历史版本和修改记录，当然这个后台就是通过 Git 来实现的。
Github 上的项目有一个新名称，叫 ”仓库“ ( repository )。说白了，一个仓库就是一个用 git 进行了版本控制的项目。
点击页面左上角的小猫图标，显示 dashboard （控制面板），日常所有的操作都在这里做。

点击New repository,新建仓库，这就到达了新建项目的页面：
注意要勾选 Initialize this repository with a README ，然后创建这个项目。也会看到 Create Repository 按钮
的上方还有两个选择框，一个是关于 .gitignore 的，另一个是关于 LICENSE 的。这两项如果选择了就是在项目中又多了
两个文本文件，一个是 .gitignore 文件，另一个是 LICENSE 文件，暂时都不选就可以，回头需要了可以自己用编辑器新建。
```
##### 编辑项目
```
创建项目完成后，就会跳转到 https://github.com/happypeter/coco 这个页面。这里的几乎每一个可以点的地方都会涉
及到一个新概念。先来瞄准一个最为重要的，叫 commit（版本提交），每次项目修改后，点击 commit 按钮就可以生成一个
新的版本。commit 英文的基本意思是执行某个重要的事情，例如 commit suicide，自我了断。但是在 git 这里，做动词
讲的时候是保存版本，当名词讲就是版本。

在 Commit new file输入框填写的是“版本留言”（ commit message ），说明一下为什么要做这次修改，一方面是跟队友
沟通的一种形式，另一方面如果项目版本多了，自己也可以用这个留言来定位特定的一次修改。第一行填写一个一行的留言，
第二行可以写详细留言，这一项是可选的。 最后，点击 Commit new file 按钮，一个新版本就做好了。如果是已新建文档
而修改版本留言，就点击"Commit changes"编辑后还可以点击 Preview changes 预览一下修改内容。

自动跳转回项目页面之后，会发现原来 1 commit 的地方，现在已经变成了下图所示的 2 commits；2 commits 是个链接，
点进入就进入了项目历史的页面。现在看到历史上有两个版本，点开上面的一个版本，或者说一个 commit，就可以看到一个
commit 所包含的信息了。重要的是 版本号 （ commit id ）。每个 commit 都有一个，是一个40位16进制数，可以用来
定位每个版本。注意一下地址栏中 url 的格式，以后只要是拿到了一个版本号，就可以照猫画虎的敲上面这样的链接来查看
这次的修改的详细内容了。

     一个 commit （版本）中最核心的内容就是这4个 w 了，谁（ who ）在什么时间（ when ）改了那些内容（ what ），
 最后一个是为什么要改（ why ），这个是版本留言发挥的作用。
```
#### 一条历史线
```
所有 commit（版本) 组成了一条历史线。那么这条线是怎么串起来的呢？随便打开一个项目，打开具体一个 commit，
通常会看到下图的内容：面显示了当前版本号（ commit id ），但是同时还显示了它之前的一个 commit 的版本号，
也就是它的“父版本”（ parent ） 的版本号。底层原理是这样，一个 commit 内部是保存了它的 parent 的版本号的，
这样就把它和它爹连在了一起，爹还有自己的爹，就会形成下图的一条历史线。

有些版本工具是以 1，2，3... 作为版本号的，但是 git 这里每个版本号都是40位十六进制数，
表面看起来稍微麻烦一些，但是实际上妙用无穷。
```
##### 第3节：本地安装 Git
```
本地安装 Github 客户端，基本的登录和克隆项目的操作。并行的，可用命令行的形式来完成相同的操作。
````
##### 安装Windows 的客户端
```
 注意：客户端之中封装了 git ，所以即使系统上没有安装 git ，客户端也是可以运行的。
 安装之后，要用 github.com 网站上的用户名密码登录，才能执行修改 github.com 上的项目数据的操作。

 客户端中 clone
 往客户端里面添加项目仓库有三种方式。点击左上角的"File"，就可以看到New（新的存储库），Add
 （添加本地路径），Clone（克隆Github项目） 这三种形式。
 
 Clone（克隆Github项目）就是从 github.com 上我们自己的账号下，直接克隆仓库到我本地机器（GitHub Desktop）。
```
##### 以下是苹果系统的安装操作，未进行实操安装。

```

安装 Git 到命令行
Mac 系统下安装 Git 可以通过 Homebrew ，把 homebrew 安装到 Mac 系统之后，执行

brew install git
然后执行

➜  ~  git --version
git version 2.5.1
如果能报出版本号，证明 git 安装已经成功了。

注意，这里安装的 git 和前面图形客户端包裹的 git 无关。

命令行中 clone 项目
clone 一个项目的关键就是要找到 github.com 上这个项目仓库的地址。地址有两种形式，一种是 SSH 的，
一种是 HTTPS 的。使用 SSH 形式的地址需要涉及到 ssh key 的配置，这个咱们的后续视频中会有专门的介绍。
所以为了简便，我们先使用 HTTPS 形式的仓库地址

git clone https://github.com/happypeter/gitbeijing.git
这样就可以了。

注意： HTTPS 形式 clone 下来的项目，如果后续修改了，每次上传都要输入密码，所以还是比较麻烦，实际中 Peter 是很少用的。
```

##### 第4节：创建本地仓库

###### 客户端中操作
```
往客户端里面添加项目仓库有三种方式。点击左上角的"File"，就可以看到New（新的存储库），Add（添加本地路径），
Clone（克隆Github项目） 这三种形式

Clone（克隆Github项目）上面第三节已描述

Add（添加本地路径），来源是你本地机器上已经存在的项目，填写它的文件夹位置，然后点击 Create&Add Repository，
如果这个项目本身就是一个 git 仓库了，就直接添加进来，如果不是，就把它变成一个 git 仓库（其实也就是在项目内
创建一个 .git 文件夹）然后再添加进客户端。

New（新的存储库） ，就是自己新建项目。填写项目名，这里就叫 GUI 吧，选择项目存放位置，然后点 Create Repository
按钮，仓库就创建好了。

命令行中操作，点击左上角第二行选择对应的库，右击弹出Open in command prompt,弹出命令提示符把一个纯粹的代码项目，
变成一个 Git 仓库（也就是有历史记录的项目），只需要执行下面的操作

cd project/
git init
这个操作产生的结果就是会在 project/ 内部创建一个 .git 的隐藏文件夹，可以查看一下

ls -a
.git
未来所有的改版历史就都会被保存到这个 .git 文件夹中了。.git 文件夹是一个项目仓库的心脏。

总结
把一个普通项目创建成 git 项目，未来就可以对它进行各种版本控制操作，以及上传到 github.com 的操作了。
```
##### 第5节：删除仓库
```
 客户端中删除
 点击左上角第二行选择对应的库，右击弹出 Remove 点击，选择删除。简单说说另外几项，Atom 是 github 
 公司开发的开源免费的代码编辑器，Terminal 是命令行终端，Finder 是文件浏览器。

 命令行中删除
 只需要：rm -r project；就一切干净了，所有因为所有的本仓库的配置，包括改版历史，包括一切一切，
 都放在了 project/.git 文件夹之中，系统让的任何其他地方都没有被修改，所以删除之后，也不会有任何污染。
 到 github.com 上删除仓库；到项目主页，例如：https://github.com/oqq5518/Liao-Zhou 。
 Settings -> Danger Zone -> Delete This Repository（设置 -> 危险区域 -> 删除这个仓库。）
```
##### 第6节:版本控制四步走
###### 第一步：编辑项目
```
先用编辑器修改一下项目。一般认为当我们要做的一个任务实现了，例如一个小功能实现了，或者一个小 bug 修复了，
这样之后，我们就可以把这次的修改内容保存成一个版本了。
```
###### 第二步：查看修改
```
但是保存版本之前，我们肯定是想要最后看一眼，我们这次都改了哪些内容。这个很有助于避免低级错误的。

图形化客户端中，操作如下。点开这个仓库中，到 Changes 一项下面，就可以看到：

命令行中要查看修改。可以这样，运行

git status
就可以看到本次的修改内容了。详细的代码还可以通过

git diff
来查看，但是 git diff 只能显示出那些已经”被跟踪“的文件的修改内容。对于”被跟踪“这个概念，后面会提到。
```
###### 第三步：添加内容
```
到客户端中，首先图中1和2两处可以看到目前项目修改了什么内容。同时可以看到1处是可以勾选的，也就是如果
我一次修改了多个文件，可以只把其中的一部分文件勾选上，添加到下一个版本（ commit ）之中。更为细致的，
你可以到右侧的显示修改内容的区域，选择一部分内容添加到下个版本中。默认行号背景是蓝色的，表示内容被选
中了，单击行号，这一行的行号背景就会变成绿色（上图2处所示），这样表示取消了选中状态。单击行号可以取消选中。

那么相同的操作命令行中怎么来作呢？应该说命令行中可以把工作做得更细，但是其实通常是没有必要的。
99%的情况下我们的想法是

不管是添加还是删除文件，都要跟踪，所有修改都添加到下一个版本中去

那么能达成这个要求的操作是

git add -A
这样就可以了。
```
###### 第四步：制作版本
```
确定要添加那些修改内容之后，就可以来执行做版本的操作了，git 这里的术语叫 commit 。

图形界面中的操作还是看上面的图。3处要填写版本留言（ commit message ） ，先用一行内容说说为啥要做这次修改，
下面的大框框里可以写详细的留言，是可选项。最后点击 Commit to master （ 把新版本做到 master 分支上 ）按钮，
一个版本就保存好了。master 是默认分支的名字，后面讲分支的时候会细聊。

命令行中这样操作。

git commit -m"版本留言”
注意：命令行中 git commit 之后还可以设置一下参数，比如 -a/-v 这些，来实现更为强大的功能，
这个后面开专门的章节介绍吧。

总结
所以总结起来，从一个 commit 到下一个 commit，也就是从历史上的一个节点到下一个节点，要经历的操作是下面四步：



重复以上四步，再作一个版本出来。这样到客户端的 History 一项下面，就可以看到历史线上已经有两个 commit 了，
点开任意一个都可以看到4个 W 。

```
##### 第7节.回滚历史
```
回滚历史操作相当于后悔药。

回滚未被上传的版本
既然历史版本都已经保存了，那么我要时空穿梭，回到任何一个版本的状态应该也是可以的。比如我刚刚做了一个版本，
就发现修改的内容有问题，想要修改一下这个版本。可以到 Changes 选项下，点击页面最底端的 undo 标签。

注意，如上图，undo 操作是对 Unsynced 的版本有效，如果版本已经同步到远端，队友已经都看见了你的这个版本，
并且可能已经在这个版本的基础上继续开发了，那么直接删除版本会给协作带来麻烦。

命令行中做相同的事情
需要执行的命令

git throwh
throwh 是一个别名，是在我的 .gitconfig 文件中设置的

[alias]
  ci = commit -a -v
  st = status
  throw = reset --hard HEAD
  throwh = reset --hard HEAD~
如果想要把最新的未被保存到历史中的修改删除，就运行 git throw 。

回滚已经上传的版本
当然，对于已经同步到远端仓库的版本，也可以用另外的方式来撤销修改内容。到 History 标签下，打开任何一个 commit ，
都可以到小齿轮中选择 Revert This Commit 来放弃里面的修改。不过这次不是删除这个版本，而是再新添加一个 commit，
里面的修改内容正好和这个 commit 相抵消。之所以不直接删除 commit，是为了避免队友对修改历史产生混淆。
```
###### 连接 Github
```
一般情况下，我的每一个项目都是两份，一份是本地仓库（ local repository ），另一份放到 github.com 上，
通常叫远端仓库（ remote repository ）。这不仅仅能让我感觉到有备份，晚上可以睡好觉了，同时这两个备份
也是可以互相同步的，要同步的内容最重要的当然是版本了。git 功能虽然多，但是说白了就是来回折腾 commit ，
要不怎么叫版本控制工具呢。

对于从 github 上 clone 下来的我自己的项目，默认的同步通道是通的，因为本地仓库中已经存放了远端仓库的地址。但是，
对于自己在本地新建的项目，需要先把它放到 github.com 上。 在客户端界面的右上角，对于从 github.com 上 clone 下
来的项目这里是 sync，但是对于 github.com 上没有对应远端仓库的本地仓库，这里就是一个 Publish 按钮。点一下，填写
项目名，是的，项目名可以跟本地项目不一样，然后添加项目描述，猛戳 Push Repository 按钮，项目就发布到 github.com
上了。如果我的用户名是 happypeter，项目名叫 coco 。那在 github.com 上链接也很优美，就是 github.com/happypeter/coco ，
现在我可以把链接分享给朋友，邀请他们一起参加项目开发。

注意在标号2的框里面，我可以把项目发布为私有项目，这个功能只对付费用户开放。

同步版本历史
在本地机器上做成一个或者是多个版本，这时候如何把这几个新版本推送（ push ）到远端仓库上面呢？在客户端中，很简单，
就是点一下右上角的 sync 按钮就好了。

也有的时候，我在 github.com 上浏览我项目的内容，突然发现一个拼写错误，也就顺手在 github.com 上点 edit 按钮，
直接修改做成版本了，这样就等于 github.com 上的远端仓库比我本地多了新版本，这时候我也需要把这个版本拽（ pull ）
到我本地机器上，也是在客户端点一下 sync （ 同步 ） 按钮就好了。

稍微梳理一下，本地和远端，也就是我自己的笔记本跟 github 服务器上两个对应仓库的沟通方式就是下面这张图

同步代码的时候，有时候会有代码冲突（ conflicts ），需要手动来解决。这个涉及到分支的概念，后面再聊。

命令行中完成
如果是从 github.com 上 clone 项目

git clone git@github.com:happypeter/coco.git
那么这样的项目内修改，然后做成版本，是可以通过 git push 命令直接上传的。

但是，如果我本地有一个新项目，就需要执行

git remote add origin git@github.com:happypeter/project.git
也就是添加远端仓库地址到本地配置中，然后才能执行

git push
上传修改内容。

总结
更多客户端使用技巧请参考官方帮助 。
```

#### 第三章：深入命令行

##### 添加 ssh key
```
如果想用 ssh 协议的形式往 github.com 上上传东西，会有“权限拒绝”这样的错误，如何解决呢？就是要靠添加 ssh key 。
```
##### 生成
```
运行
ssh-keygen
这样可以在 ~/.ssh 中看到这一对儿 key 了。
```
##### 添加
```
 到用户个人主页 -> Edit Profile -> SSH Key
```

##### ~/.gitconfig
```
~/.gitconfig 文件内容如下：

[user]
  email = happypeter1983@gmail.com
  name = Peter Wang
[core]
  editor = vim
[alias]
  ci = commit -a -v
  st = status
  br = branch
  throw = reset --hard HEAD
  throwh = reset --hard HEAD~
[push]
  default = simple
  粘贴有自动缩进，敲：set paete
  敲i，插入模式
  然后
  ctrl+v 粘贴
  就不会有自动缩进了
  ：wq  保存退出
```
##### GitHub退出登录账号的路径

```
操作过程：
1.在登录的GitHub的左上角中，点击”File”按钮

2.在弹出的”File”下拉框中选择”Options”

3.在”Options”弹窗中，点击”Sign out”退出按钮
```
