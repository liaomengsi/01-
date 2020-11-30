# 01-

## 作业一：虚拟机

**目录**

**第一部分：创建及配置虚拟机**

**第二部分：查看主机和虚拟机的IP地址**

**第三部分：互相ping IP地址**

**第四部分：开通http server服务及访问**



### 第一部分：创建及配置虚拟机

#### 一、创建

1.在VirtualBox的官网： [Oracle VM VirtualBox](https://www.virtualbox.org/) 直接下载Windows版本的软件，安装。

2.新建一个桌面版虚拟机，若是服务器版本，则只有命令行，所以使用有图标的桌面版会更适合初学者，更方便。将虚拟机命名为202010.19。

#### 二、配置

1.创建之后需要更改配置，网络设置为**桥接网络**，使得在内网中主机和虚拟机可以相互访问。

2.在虚拟机**关闭**的状态下，给虚拟机分配光驱，则在：存储——控制器SATA端口增加光盘镜像文件ubuntu-20.04.1-desktop-amd64.iso。![1606730672728](C:\Users\63407\AppData\Roaming\Typora\typora-user-images\1606730672728.png)

3.设置好之后的界面如下：![1606730622453](C:\Users\63407\AppData\Roaming\Typora\typora-user-images\1606730622453.png)

4.正常启动虚拟机，接着是安装Ubuntu虚拟机，全部选择默认安装即可。安装所需要的时间比较久，期间尽量不要关机或者断开网络连接。

#### 三、出现的问题及解决办法

1.在启动虚拟机时，曾出现了以下两种情况：

（1）点击“启动”直接显示出错，此时我的解决办法是再重新创建一个虚拟机，若再出现这个情况，则卸载全部与virtualbox有关的文件，重新下载安装。

（2）第二种是点击“启动”可以正常运行，但是在点击安装、创建用户名时，出现光标和键盘在虚拟机界面中无法使用的情况，另外此时虚拟机运行的界面中，有部分内容未显示出来，鼠标也无法拖动查看，解决办法是强行关闭虚拟机，重启。

2.成功安装虚拟机之后的初始界面如下![](C:\Users\63407\Pictures\分布式作业相关图片\虚拟机初始界面.png)

### 第二部分：查看主机和虚拟机的IP地址

1.安装虚拟机之后我做的第一件事是打开终端Terminal，输入ifconfig查看虚拟机IP地址，结果出现以下报错情况：ifconfig未安装![1606734451788](C:\Users\63407\AppData\Roaming\Typora\typora-user-images\1606734451788.png)

2.按照提示sudo apt install net-tools安装ifconfig,结果还是报错，![](C:\Users\63407\Pictures\分布式作业相关图片\微信截图_20201130191054.png)

3.所以就到网上寻找解决办法，发现第一步是检查网络是否连接成功，在terminal输入ping www.baidu.com,若无报错则表明网络连接无问题。所以我就按照提示ping百度的网址，出现错误提示：Temporary failure in name resolution

4.接着再上网查看出现类似错误的解决办法，按照多种解决方法来操作，仍然无解。后来是在课上询问老师之后，才发现：主机连接校园网，虚拟机显示已连接网络，但其实未连接成功，需要在虚拟机的网页中再次登入校园网的账号密码；第二种解决办法是使用个人的wifi热点。我选择了后者，再次ping baidu.com 时成功了！

#### 第三部分：互相ping IP地址

1.为实现主机与虚拟机的互相ping通IP地址，我们需要知道相互的IP地址。

（1）查看虚拟机的IP地址：输入sudo apt install net-tools安装ifconfig，成功安装之后，输入ifconfig，即可查看虚拟机的IP地址：192.168.43.85![](C:\Users\63407\Pictures\分布式作业相关图片\微信截图_20201130200804.png)

（2）查看主机的IP地址：打开主机终端win+R，cmd，输入ipconfig得到主机的IP地址：192.168.56.1![](C:\Users\63407\Pictures\分布式作业相关图片\主机ipconfig.png)

2.主机和虚拟机的IP地址都知道之后，在虚拟机上ping主机，输入ping 192.168.56.1,得到结果如下：![](C:\Users\63407\Pictures\分布式作业相关图片\虚拟机ping主机.png)

3.主机ping虚拟机，输入ping 192.168.43.85，得到结果如下：![](C:\Users\63407\Pictures\分布式作业相关图片\主机ping虚拟机.png)

#### 第四部分：开通http server服务及访问

1.利用python3自带的http模块，在主机中开通http server 服务。输入python3 -m http.server 8010，其中端口号8010可以自己取一个，则得到一个IP地址：http://0.0.0.0:8010/

![1606738781614](C:\Users\63407\AppData\Roaming\Typora\typora-user-images\1606738781614.png)

2.用浏览器打开http://0.0.0.0:8010/，即出现下图：实现了从主机通过浏览器访问虚拟机中的http服务中的HTML文件。

![1606739436810](C:\Users\63407\AppData\Roaming\Typora\typora-user-images\1606739436810.png)






