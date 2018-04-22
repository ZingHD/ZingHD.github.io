这篇博客可以解决
**1.如何安装win10,ubuntu双系统**
**2.如何使用win10引导Ubuntu，并且设置win10引导界面**

#win10,ubuntu双系统的安装
为什么要装双系统，之前用的虚拟机，但是虚拟机没有显卡，使用gazebo之类的3D仿真软件经常出问题，所以选择装双系统。
强烈建议安装**Ubuntu16.04的64位系统**，可以使你之后的开发环境搭建非常顺利。

##0.工具
硬件：一个空的U盘(4G及以上)
软件：[EasyBCD2.3](https://pan.baidu.com/s/1lwPUM-a_Vi_cgVe3WC264g)密码tb8w,[傲梅分区助手](https://www.disktool.cn/download.html),[UltraISO](http://cn.ultraiso.net/xiazai.html),[Ubuntu系统](https://www.ubuntu.com/download/desktop)
##1.创建Ubuntu分区
###1）使用win10自带的磁盘管理
按住Win + X，选择“磁盘管理”
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/win10%E8%87%AA%E5%B8%A6%E5%88%86%E5%8C%BA1.PNG)
选择剩余空间较大的可分配磁盘，右键并选择“压缩卷”，这里选择压缩E盘50G左右的空间
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/win10%E8%87%AA%E5%B8%A6%E5%88%86%E5%8C%BA2.PNG)
点击“压缩”之后，E盘后部出现黑色的50G“未分配空间” 
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/win10%E8%87%AA%E5%B8%A6%E5%88%86%E5%8C%BA3.PNG)
至此，磁盘分区过程完成.这种方法参考[相关博客](https://blog.csdn.net/pop_rain/article/details/70477085)
###2）使用傲梅分区助手
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/aomeifenqu.png)

 **给磁盘分区有很多种方法，可以自行选择，分区的目的是为了给Ubuntu系统分配安装空间，建议40G及以上。**

##2.制作Ubuntu的启动U盘
**制作启动U盘会格式化U盘，注意备份文件。**
将U盘其插入电脑,进入UltraISO，
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/UISO1.png)

打开下载好的Ubuntu镜像文件(ubuntu ISO文件)。
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/UISO2.png)

保持默认设置即可
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/UISO33.png)

点击写入
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/UISO4.png)
Ubuntu的启动U盘制作完成，其实非常简单，就是打开软件，选择镜像文件，点击写入即可。[图片来源博客](https://blog.csdn.net/pop_rain/article/details/70477085)

##3.安装系统
首先需要进入bios设置优先u盘启动。
不同品牌的电脑进入bios的方式不同，可以自行百度。
在bios中找到USB HDD选项用Tab键把它调整到第一的位置即可
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/IMG_20180422_095036.jpg)

设置完成后，插入U盘然后重启电脑，就会进入系统安装界面

![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/U1.png)
建议都不要选，否者会需要联网下载，会很慢。
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/U2.png)

<font color=red>注意这里选其他选项</font>
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/u3.png)

点击的“+”创建4个主要的基础分区（这里之前未分配的50G就是给ubuntu系统的50G），按以下参数设置4个主要的基础分区：

|大小 |新分区的类型|新分区的位置|用于|挂载点|用途|
|---- |----------|-----------|---|------|----|
|10G |主分区|空间起始位置|Ext4日志文件系统 |/|用于存放系统相当于win10的C盘|
|4G|逻辑分区|空间起始位置|交换空间|/swap|相当于电脑内存|
|200MB|逻辑分区|空间起始位置|Ext4日志文件系统|/boot|引导分区|
|所有剩余的空间|逻辑分区|空间起始位置|Ext4日志文件系统|/home|用户存储数据用|
我的系统安装完后 主分区使用了1.31G,boot分区使用了151.72M,所以如果你硬盘有限至少也要大于这个标准。
####主分区 /
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/U5.png)
####交换空间 /swap
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/U6.png)
####引导分区 /boot
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/U7.png)
####用户数据 /home
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/U8.png)

###用win引导Ubuntu！
<font color=red>安装启动引导设备的参数选择：与/boot所在的编号一致。</font>
**如果这步忽略了，你就用了Ubuntu系统来引导Windows了**
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/U9.png)

之后就没坑了
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/U11.png)
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/U12.png)
记住你的密码别忘了。
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/U13.png)
到这里Ubuntu已经安装好了，可以重启，然后拔掉U盘，如果你按照我的步骤，重启会进入**win10系统**。

##4.设置win10引导Ubuntu
一定要用EasyBCD2.3
重启在win10下进入EasyBCD，选择“添加新条目”，选择Linux/BSD操作系统，在“驱动器”栏目选择接近200M（就是boot的分区）的Linux分区，点添加条目
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/EasyBCD1.png)
编辑引导菜单，勾选Use Metro bootloader
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/EasyBCD.png)

重启电脑，恭喜你，Win10和Ubuntu的双系统已经完成安装
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/win10%E5%BC%95%E5%AF%BC.jpg)

用Windows引导Ubuntu最大的好处就是，当不再需要Ubuntu的时候，直接在Windows磁盘管理中将其所在所有分区删除，然后将EasyBCD中对应条目删除即可。

写教程真心不容易，感谢网络上分享教程的大神，[折腾日记]这个栏目以后用来记录一些教程工具的折腾过程，目的是同样的坑绝不踩两遍。如果碰巧解决了你的问题，请点赞转发分享一下哟。

预告：系统装好了接下来当然是为Ubuntu设置科学上网，然后安装Pixhawk编译环境，很快更新，尽情期待。


#踩过的坑
引导设置错误，重启就会进入这个界面，这是Ubuntu引导win10,如果你在这种情况删除Ubuntu的分区，你会发现win10也进不去了，需要修复win10的引导。我为此又重装了一遍。。。。。
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/ubuntu%E5%BC%95%E5%AF%BC.png)
重启进入win10但是界面太丑，因为用了EasyBCD2.2没有Use Metro bootloader选项
![](https://raw.githubusercontent.com/ZingHD/Markdown_picture/master/win10ubuntu%E5%8F%8C%E7%B3%BB%E7%BB%9F/win10%E5%BC%95%E5%AF%BC%E9%BB%91.jpg)

参考资料
https://www.cnblogs.com/zhuyinxiaozi/p/5424284.html
https://blog.csdn.net/pop_rain/article/details/70477085
https://jingyan.baidu.com/article/3c48dd348bc005e10be358eb.html
