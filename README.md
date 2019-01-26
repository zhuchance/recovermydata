# 恢复误删除的数据 recovermydata 
这个项目是帮助程序员朋友们数据恢复的.This case is to help programmers to recover data.

*最近有很多朋友问到数据误删除怎么办*`

说来有缘第一个github上的fork的项目就是WinHex，熟悉数据恢复的朋友都知道这是一款最强大的数据恢复软件没有之一，庆祝一下微软开放了无限的私人仓库，我决定把数据恢复的一些经验和技巧开源出来与大家分享，当然这中分享是面对有一定技术能力的同行(程序员)。如果实在是搞不定发邮件给我，我很乐意帮忙。
 看完这个文档程序员朋友们写程序的时候可以明了一下数据存储的方式和基础原理。

  
#### 磁盘的基础格式
  1.磁盘：以温切斯特硬盘(实际上到目前为止大部分数据都还是存在传统硬盘上)为例，核心都是一个圆碟都磁盘加上一个来复运动的磁头。
  2.磁盘格式：一下的文档依据FAT32格式为案例讲解，实际上现在windows系统下几乎都是ntfs格式Linux系统下磁盘的格式比较多，MacOs现在只用HFS+或者APDFS。
  3.磁盘上物理结构：温切斯特磁盘是一种使用磁介子记录信息的存储工具，磁极的N极和S极刚好对应计算机里面的二进制0和1。
  4.文件逻辑结构：几乎所有的文件系统和数据库都使用了类似B+二叉树的数据结构，为了方便遍历文件。
  5.盘面、磁道、扇区，结合图片来看，由于温切斯特硬盘的结构注定了数据不可能是顺序排列的，硬盘厂家出厂的时候会做一次低级格式化，这个不在本次讨论的范畴，其中一条作用是把不健康的磁区屏蔽掉。
  
  
#### winhex是一个能直接查看物理磁盘数据的工具。
    举个栗子：修复一个格式化的FAT32格式的u盘
    1.人为破坏存储模拟格式化(这里使用winehe把mbr填0，这是一种比格式化来的更凶的操作，当年chi病毒就是这么搞的哦)：![image](https://github.com/zhuchance/recovermydata/blob/master/images/format.png)
    2.根据fat表找到对应扇区![image](https://github.com/zhuchance/recovermydata/blob/master/images/winhex1.png)
    3.根据对应数据修复mbr数据![image](https://github.com/zhuchance/recovermydata/blob/master/images/winhex1.png)
    4.数据修复，注意正常的数据恢复取证流程是不会对原数据盘做任何写操作，所有的操作都是基于物理镜像来做的。winhex可以很方便的做物理镜像，Linux或者mac下面可以直接使用dd命令做物理字节级别拷贝
    