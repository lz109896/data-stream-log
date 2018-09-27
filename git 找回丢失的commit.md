## 事件背景：已经提交了一个新增的文件，但是执行  git rebase （复位基底），导致本地代码丢失，找回巨费时，特记录如下;
```
执行：git reflog       ----查看提交记录；挽回错误的重置，查看命令历史，用来记录你的每一次命令
git reset --hard (+rebase: updating HEAD 版本代码号)  
git cherry-pick (+commit: ioc 版本代码号) 
```
```js
PS D:\yujie_web> git reflog
a012b29 (HEAD -> diff, master) HEAD@{0}: checkout: moving from master to diff
a012b29 (HEAD -> diff, master) HEAD@{1}: rebase finished: returning to refs/heads/master
a012b29 (HEAD -> diff, master) HEAD@{2}: rebase: table
776fe8d (origin/master, origin/HEAD) HEAD@{3}: rebase: checkout refs/remotes/origin/masterkout refs/remotes/origin/master
49a3524 HEAD@{4}: rebase: updating HEAD
49a3524 HEAD@{5}: rebase: aborting
1793050 HEAD@{6}: commit: ioc                                                           er
776fe8d (origin/master, origin/HEAD) HEAD@{7}: rebase: checkout refs/remotes/origin/master
49a3524 HEAD@{8}: commit: table
b4ee366 HEAD@{9}: rebase finished: returning to refs/heads/masterb4ee366 HEAD@{10}: rebase: vscode 配置更改
d7b38ef HEAD@{11}: rebase: checkout refs/remotes/origin/master
a1215cd HEAD@{12}: commit: vscode 配置更改6fa7e13 HEAD@{13}: clone: from http://git.code.oa.com/guanjia-innovation/yujie_web.git
PS D:\yujie_web> git reset --hard 49a3524HEAD is now at 49a3524 tablePS D:\yujie_web> git cherry-pick 1793050
error: could not apply 1793050... ioc
```
```js

备注：        
index，执行git add的操作，会对文件创建索引，所有被跟踪的文件索引会放入index，表示文件被修改待提交      
working tree，当前工作区，被修改但未被add的文件，存储在工作区        
ORIG_HEAD,用于指向前一个操作状态,每次的commit或者pull或者reset，git 都会把老的HEAD拷贝到.git/ORIG_HEAD，通过对ORIG_HEAD的引用可    
以指向前一次的操作状态 

1、hard(慎用) 重设index和working tree,所有改变都会被丢弃，包括文件的修改、新增、删除等操作，并把HEAD指向<commit>， 
因此通过git log查看版本提交记录，被reset的版本记录会被丢弃，但可以通过git reflog查看 

2、soft 不重设index和working tree,仅仅将HEAD指向<commit>,表示已经commit的文件会取消commit, 通过git status查看，
文件会处于待commit状态“Changes to be committed” 

3、mixed(默认) 重设index,但不重设working tree,表示已经被add的文件，被取消add， 通过git status查看，文件会处于待添加索引状态 
“Changes not staged for commit” 

4、merge 重设index，重设working tree中发生变化的文件，但是保留index和working tree不一致的文件 

5、keep 重设index，重设working tree中发生变化的文件

```















