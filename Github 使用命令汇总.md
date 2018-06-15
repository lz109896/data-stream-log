## 开始使用git：

在本机上安装git，http://progit.org/book/

使用github充当远端服务器，托管本地代码：www.github.com

在github上注册好帐号，创建一个仓库，就可以将本地仓库托管上去了

剩下的就是从原理上学习git，熟练掌握git的常用命令，不懂的就git --help。
   
## git常用命令及功能

git常用命令：

git config ：配置git

git add：更新working directory中的文件至staging area。

git add .更新所有的文件

git commit：提交staging area中的文件至git repository中。

git commit -m 'message' ：提交到主分支

git status：查看状态

git diff：查看改动情况

git remote：查看远端服务器别名，加上-v显示url信息

git remote add server_url local-alias：添加远端服务器

git clone project_url local_alias：克隆项目到本机中

git push server_url/local-alias：更新远端服务器仓库

git pull server_url/local-alias：更新本地服务器仓库

在本次使用github过程中，暂时遇到现在这些问题，感觉还有很多不懂的地方，有待改进。


## 安装git for windows.

现在本地创建一个不带中文的文件夹，右键会出现git bash here 点击(快捷打开一个本地仓库，打开另外一个仓库就在那个仓库右键这个)

进行初始化设置，用户名及邮箱。打开git bash，执行命令：

$ git config –global user.name your_name

$ git config –global user.email your_email

先输入$ssh-keygen –t rsa –C “your_email”,注意ssh-keygen之间是没有空格的,其他的之间是有空格的

回车之后,会出现一行,让你输入一个保存密钥的地方,括号里面是它默认的位置，这里会让你输入几次内容，都不用输入，直接回车就可以了。

回车之后,这样密钥就生成了,可以打开id_rsa.pub（位置根据你的电脑来看）来查看,我使用的是记事本直接打开的这个文件,里面的所有内容就是这个密钥,一会需要使用的时候,就直接全选复制就可以了

在转到github网站上去配置一下ssh key,点击箭头指示的三角图标，选择Settings，然后点击左侧的SSH Keys，之后点击右侧的Add SSH Key，这样就会出现添加SSH Key的界面，在Title这一栏填一个名字，名字随意起，之后打开刚才生成的那个文件id_rsa.pub，全选复制里面的内容到Key这一栏中，点击Add Key按钮完成操作，这时你填的邮箱会收到一封确认的邮件，不用管它

git就配置好了接下来开始创建仓库

$ git init                  //初始化仓库，会再本地出现一个隐藏文件.git

$ touch README              //向.git 提交README文件

$ git add README            //更新README文件

$git commit -m "写入注释"   // 提交更新，并注释，最好的不要省略-m"注释"可以帮助自己和别人来了解修改了什么

好了，接下来去 github 网站创建一个仓库，名字和你的本地仓库是一致的（如果下面的README你有打勾就可以省略第二第三行代码）,找到右边中间有一个SSH ，把SSH输入到git bash里面，比如我的：

$git remote add origin git@github.com:lz109896/web-learn.git  //链接远程github仓库

$git push -u origin master //将本地仓库的东西更新到 github 仓库中的 master 分支，首次需要添加-u 之后就不需要了。

这样 git 和 github 就初步结合了。

以后可以在本地修改完代码或者添加文件就先

$git add //更新

$git commit -m "注释" //提交并注释

$git push origin master //合并到远程仓库中

接下来就是一直小提示
在 github 网页中更改，要同步到本地仓库,那么就用 $git pull origin master 分支合并

## 删除远程仓库文件就使用如下命令

$git rm -rf task //例如删除task文件

$git add -A //更新

$git commit -m "注释" //提交并注释

$git push origin master //同步分支
