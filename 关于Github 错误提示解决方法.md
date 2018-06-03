####  Github 创建一个库
##### 1.首先在 Github 创建一个库，在此示例库名为：test,
##### 2.创建完成后会有显示通过什么途径添加文件

* 在命令行上创建一个新的存储库的命令：
```
 echo "# test" >> README.md
 git init
 git add README.md
 git commit -m "first commit"
 git remote add origin git@github.com:lz109896/test.git
 git push -u origin master
```
* 从命令行中推送现有的存储库的命令：
```
 git remote add origin git@github.com:lz109896/test.git
 git push -u origin master
```
* 从另一个存储库导入代码：
```
 可以使用来自Subversion，Mercurial或TFS项目的代码初始化此存储库。
 点击导入代码，根据旧版本库的克隆网址，点击开始导入即可
```

#### 第一次提交本地项目（工程）到 Github

##### 1.本地项目的库名为 Java-datum
##### 2.打开 Git Bash，并切换到 Java-datum，查看是否有对应的提交文档

![]()

##### 3.在 Git Bash 上执行创建一个新的存储库的命令:
```
 echo "# test" >> README.md
 git init 
 git add README.md
 git commit -m "first commit"    ------当执行到这里时下一步可能就会报错了
```
##### 4.当输入$ Git remote add origin git@github.com:djqiang（github帐号名）/gitdemo（项目名）.git 
```
  提示出错信息：fatal: remote origin already exists.
  解决办法如下：
  1、先输入$ git remote rm origin
  2、再输入$ git remote add origin git@github.com:djqiang/gitdemo.git 就不会报错了！
  3、如果输入$ git remote rm origin 还是报错的话，error: Could not remove config section 'remote.origin'. 
     我们需要修改gitconfig文件的内容
  4、找到你的github的安装路径，我的是
     C:\Users\ASUS\AppData\Local\GitHub\PortableGit_ca477551eeb4aea0e4ae9fcd3358bd96720bb5c8\etc
  5、找到一个名为gitconfig的文件，打开它把里面的[remote "origin"]那一行删掉就好了！
```
##### 5.如果输入$ ssh -T git@github.com
```
    出现错误提示：Permission denied (publickey).因为新生成的key不能加入ssh就会导致连接不上github。
    解决办法如下：
    1、先输入$ ssh-agent，再输入$ ssh-add ~/.ssh/id_key，这样就可以了。
    2、如果还是不行的话，输入ssh-add ~/.ssh/id_key 命令后出现报错Could not open a connection to your 
       authentication agent.解决方法是key用Git Gui的ssh工具生成，这样生成的时候key就直接保存在ssh中了，
       不需要再ssh-add命令加入了，其它的user，token等配置都用命令行来做。
    3、最好检查一下在你复制id_rsa.pub文件的内容时有没有产生多余的空格或空行，有些编辑器会帮你添加这些的。
```
##### 6.如果输入$ git push origin master
```
    提示出错信息：error:failed to push som refs to .......
    解决办法如下：
    1、先输入$ git pull origin master //先把远程服务器github上面的文件拉下来
    2、再输入$ git push origin master
    3、如果出现报错 fatal: Couldn't find remote ref master或者fatal: 'origin' does not appear to be a git 
    repository以及fatal: Could not read from remote repository.
    4、则需要重新输入$ git remote add origingit@github.com:djqiang/gitdemo.git
```
##### 7.如果输入：git push -u origin master 
```
    一直提示出错信息：fatal: Could not read from remote repository.拒绝访问权限时
    解决办法就是需要全部重新检查一遍：
    1.查看远端地址 :git remote –v 
    2.查看配置: git config --list
    3.检查自己的 Github 上是否添加密钥？:ls -al ~/.ssh
      如果没有密钥就要生成密钥：
      查看：https://help.github.com/articles/checking-for-existing-ssh-keys/
      生成：https://help.github.com/articles/generating-a-new-ssh-key-and-adding-it-to-the-ssh-agent/#adding-your-ssh-key-to-the-ssh-agent      
    4.有密钥会有类似以下文档id_dsa.pub、id_ecdsa.pub、id_ed25519.pub、id_rsa.pub 
    5.会在本地C:\Users\你的用户名.ssh生成文件夹，里面有id_rsa和id_rsa.pub两个文件 
      然后复制id_rsa.pub文件里面的内容，到https://github.com/settings/keys新建一个，
    6.完成以后，验证下这个key是不是正常工作：
    $ ssh -T git@github.com
    Attempts to ssh to github
    7.当最后输入：git push -u origin master，
      弹出：Enter passsphrase for key '/C/Users/Administrator/.ssh/id_rsa':  时
      一定是输入你刚才设置密钥的密码，要记得保存哟！！！      
    8.如果，看到：
      Hi xxx! You've successfully authenticated, but GitHub does not # provide shell access.
      恭喜你，你的设置已经成功了。
```
##### 8.在新增密钥时，不要搞错对象
```
     1.不要进到某个库的设置中进行添加，页面例如：https://github.com/lz109896/Web-datum/settings/keys
     2.需要点击 Github 头像==》设置，点击 SSH and GPG keys 中进行配置；例如:https://github.com/settings/keys   
```
##### 9.使用git在本地创建一个项目的过程
```
    $ makdir ~/hello-world    //创建一个项目hello-world
    $ cd ~/hello-world       //打开这个项目
    $ git init             //初始化 
    $ touch README
    $ git add README        //更新README文件
    $ git commit -m 'first commit'     //提交更新，并注释信息“first commit” 
    $ git remote add origin git@github.com:defnngj/hello-world.git     //连接远程github项目  
    $ git push -u origin master     //将本地项目更新到github项目上去
```  
  
  





