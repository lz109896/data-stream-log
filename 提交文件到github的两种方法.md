## 提交文件到github的两种方法
```
方法一：在github中创建代码仓库，这个仓库中几乎是空白，本地工程中有完整的需要提交的代码，
通过git init、git remote add、git push等命令来完成。

方法二：在github中创建代码仓库，或者代码仓库已经创建了，然后通过git clone、git push等命令来完成。
通常这种方法是我们使用最多的。

方法一和方法二的区别，是方法一中的本地工程目录一开始不是git仓库，也不是git clone而来的，只是普通的目录。
方法二中的目录是通过git clone而来的，是跟远程github上的仓库关联的。

其实，也可以使用方法二将本地工程目录提交到github，即先git clone [github_repository_url]，然后将本地工程目录中的
文件添加到克隆出来的目录中，然后再执行git add、git commit和git push等一系列操作。
```
#### 需要注意的是，文本所说的提交到github，只是提交到自己github账号下的代码仓库中。

### 方法一
```
简要步骤如下：

登陆github，创建git仓库。记此git仓库的地址为[github_repository_url]，
例如git仓库的地址：https://github.com/galian123/nodejs_http_server

在本地的工程目录执行git init，此工程目录是要提交到github的。git init是将本地的工程目录作为本地的git仓库。 
注：下面的git命令都是在此工程目录中执行的

执行git add .，将本地的工程目录（包括子文件）都添加到本地的git仓库

执行git commit -m "write some comment"，将本地的工程提交到本地的git仓库

执行git remote add origin [github_repository_url]，将本地仓库与github上的仓库关联起来。 
可以通过git remote -v查看github上的仓库地址。

执行git pull origin master同步github仓库和本地仓库

执行git push origin master将本地工程提交到github

具体的例子： 将本地nodejs服务器的代码提交到github:https://blog.csdn.net/u013553529/article/details/58350653

github官网的说明：Adding an existing project to GitHub using the command line
:https://help.github.com/articles/adding-an-existing-project-to-github-using-the-command-line/
```
### 方法二
```
简要步骤如下：

登陆github，创建git仓库。或者github中已经有了一个git仓库（之前创建的，或者是从别人那fork出来的）。 
记此git仓库的地址为[github_repository_url]。

执行git clone [github_repository_url]，将github上的仓库克隆到本地。

进入到克隆的仓库目录 
注：如果进入的目录是很久之前克隆出来的，此时要先git pull以更新到github中的最新文件。

将修改的或者新加的文件放入克隆的仓库目录中

执行git add .将改动添加到本地仓库。

执行git commit -m [your_comment]将改动提交到本地仓库。

执行git push origin [your-branch]将本地的改动提交到github中。如果提交到主分支上，则[your-branch]为master。
即执行git push origin master
```
