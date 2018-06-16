#### 第一章：课程介绍
##### Linux的八项基本操作 ： 
###### 1.终端配置  用户权限  重定向   软件安装 
###### 2.搜索  进程 网络操作
###### 3.脚本编程

#### 第二章：命令行
##### 第一节：选择操作系统
###### redhat(红帽)大企业服务，策略保守、fedora()、centOS（）
###### 建议选择ubuntu来学习及工作；（有阿里云、DigitalOcean、linode、amazon的支持）
###### ubuntu不仅是流行的服务器平台，也是优秀个人开发平台
###### ubuntu系统是免费的，推荐2012.04月的版本
官网下载网址：https://www.ubuntu.com/download/desktop/thank-you?country=CN&version=18.04&architecture=amd64

###### 安装视频参考google
###### 不错的linux文档:ttp://billie66.github.io/TLCL/book/chap03.html
###### linux有许多的版本，我们这里选择ubuntu来学习下载地址是releases.ubuntu.com；百度一下也一样

##### 第二节：设置终端软件
###### 敲terminal查找终端软件
###### 点击Edit，点击profiles,进行设置；NEW,可以改字体，改颜色，选中imooc,每次都可以快速启动进入，设置后要关掉重启。
###### 敲ctrl+alt+t打开终端
###### 敲python能够进入python语言的编程环境中；ctrl+d退出；
###### 敲clear或者 ctrl+l清屏

##### 第三节：如何学习命令
###### 命令提示符解剖：liaozhou@dog:~s
liaozhou:是用户名username
dog:机器名machinename
~:当前工作目录（用户主目录）
$：$符号后面输入命令
###### madir 新建
###### rm -r 删除

##### $ rm -r ttt/  解剖
rm :命令本身
-r：参数（有时候需要加）
ttt/：操作对象
##### 建议通过教程学习linux，开发人员水平看他使用googlede 水平
参考：http://billie66.github.io/TLCL/book/index.html；推荐查看第二、第六章
##### 终端也可以敲：man 看到使用手册

#### 第三章：linux在文件系统中跳转
##### 第一节：文件系统树结构
###### windwos linux 分区：sda1 sda2 是倒置的一棵树
sda1 挂载 /（后面存放东西在sda1中）
sda2 挂载在 /里的/home （/home后面存放的东西在sda2中）

##### 第二节：绝对路径和相对路径
###### 绝对路径从根目录开始    cd /bin/home/liaozhou/files(一层层往下到最后要打开的那个文件夹)
###### 相对路径从当前目录开始   cd ./files(也可以cd files)（直接进入到要打开的根目录）
###### .当前目录
..上一个目录
../..上上级目录

##### 第三节：cd命令
###### pwd显示当前目录，cd改变当前目录。
###### “cd -”也可以返回刚才的目录
###### 当备选项只有一个是tab可自动补齐
###### 敲两次备选项就可以查看全部对应的选项，再次敲备选项tab可自动补齐  （也称为虚化查找）

#### 第四章：linux操作文件和目录
参考文档：http://billie66.github.io/TLCL/book/index.html

cp -r dir1/dir2   表示拷贝dir1并新建dir2
cp -r dir1 mydir/ 表示拷贝dir1到mydir，mydir里面就会多一个dir1

#### less命令

Ctrl--缩小字体

Ctrl++增大字体

j 向下滚屏

k 向上

/字符 字符查找 n查找下一处

敲两下g 到文件头

敲两下G 到末尾

less 工具也是对文件或其它输出进行分页显示的工具，应该说是linux正统查看文件内容的工具，功能极其强大。less 的用法比起 more 更加的有弹性。 在 more 的时候，我们并没有办法向前面翻， 只能往后面看，但若使用了 less 时，就可以使用 [pageup] [pagedown] 等按 键的功能来往前往后翻看文件，更容易用来查看一个文件的内容！除此之外，在 less 里头可以拥有更多的搜索功能，不止可以向下搜，也可以向上搜。

#### 1．命令格式：

less [参数]  文件 

#### 2．命令功能

less 与 more 类似，但使用 less 可以随意浏览文件，而 more 仅能向前移动，却不能向后移动，而且 less 在查看之前不会加载整个文件。

#### 3．命令参数：

rm a* 删除所有以开头的文件
rm -* 删除所有
rm -rf* 删除所有

wget http://imooc....  下载网站的主页

-a 显示所有

-b <缓冲区大小> 设置缓冲区的大小

-e  当文件显示结束后，自动离开

-f  强迫打开特殊文件，例如外围设备代号、目录和二进制文件

-g  只标志最后搜索的关键词

-i  忽略搜索时的大小写

-m  显示类似more命令的百分比

-N  显示每行的行号

-o <文件名> 将less 输出的内容在指定文件中保存起来

-Q  不使用警告音

-s  显示连续空行为一行

-S  行过长时间将超出部分舍弃

-x <数字> 将“tab”键显示为规定的数字空格

/字符串：向下搜索“字符串”的功能

?字符串：向上搜索“字符串”的功能

n：重复前一个搜索（与 / 或 ? 有关）

N：反向重复前一个搜索（与 / 或 ? 有关）

b  向后翻一页

d  向后翻半页

h  显示帮助界面

Q  退出less 命令

u  向前滚动半页

y  向前滚动一行

空格键 滚动一行

回车键 滚动一页

[pagedown]： 向下翻动一页

[pageup]：   向上翻动一页

#### 4.解压及压缩包命令
zip包下：
解压缩：unzip + filename .zip
删除原有zip包：rm filename.zip 
跳转到该文件里面：cd filename/
查看源码：ls
重新打包：zip -r filename2.zip 文件目录/

zxvf、zcvf：
x：解压缩
c:压缩（compress）

 .gz 压缩包：
解压缩：tar zxvf 加上包
删除压缩包：rm 包
压缩：tar zcvf filename2 目录名/
 .bz2：
解压缩： tar jxvf 包名
压缩：tar jcvf filename2 目录名/

打印文件：echo *.html
创建文件：touch a.txt
>a.txt
创建目录： mkdir dir
查看文件：cat file
查看文件类型：file a.txt
###### 
