# Linux&Shell_notes

#### 1.操作系统的多个层面:

硬件 -> 内核 -> 系统调用 -> 应用程序

#### 2.linux设备即文件的表现---设备的"文件名"

设备所在目录: /dev

> dev = device (另外, dev在其他地方常常有developer的意思)

常用的:

* IDE硬盘 /dev/hd[a-d]
* SATA硬盘 /dev/sd[a-p]
* 鼠标 /dev/mouse
* 打印机 /dev/lp 或者 /dev/usb/lp

*和英文*

*差异化: lp 与 printer*

*统一化: harddisk 和 hd; sd与"super"disk mouse*

#### 3.磁盘的重要部分

* 主引导分区 MBR( Master Boot Record)

> 用于安装引导分区

* 分区表 Partition table

> 用于记录分区信息

*这和计算机结构:*

*差异化:计算机是数据和程序联动,且存储在一起,并被存入内存当中,被cpu处理执行.*

*统一化:数据和程序.*

#### 4.磁盘*扇区*,*磁道*和*柱面*的简单概念

* 磁道是一个个同心圆
* 扇区是同心圆上的一段段圆弧
* 相同位置的磁道: 柱面

*三者与名称上的差异化:磁道有很多,这与一个圆本身...   另外,柱面却只是多个圈圈*
*统一化:扇区的确是一个小扇区,因为磁道是有一定宽度的,这也就与柱面统一了*

#### 5.分区

主分区和扩展分区

主分区, 扩展分区的信息被记录在"主分区表"

> 也就是说, 主分区和扩展分区都是同种"层次"的分区, 只是功能有些许不同而已.

而逻辑分区正是扩展分区的功能所在.

> 而逻辑分区的分区信息记录在别处

*三种分区概念和地块的*
*差异化:貌似主和扩展 和地块上的概念略有不同*

*统一化:逻辑分区和逻辑上的分区是非常吻合的*

> 注意: sda1-sda4都会被保留给主分区使用, 所以第一个逻辑分区一定是从5开始. 另外就是, 扩展分区只能有一个.

#### 6.电脑开机流程

1. BIOS
2. MBR
3. Boot Loader
4. Kernel

> 前两个提供自检和基本启动信息, Bootloader (在MBR内部,是由操作系统安装上去的),作为一个启动器启动内核(也就是系统本身)
>> 这和火箭, 差异处: 火箭没有自带的BIOS和MBR.      
>> 统一处: 启动过程十分类似. 

#### 7.常用文件操作指令

1. mv
> 也就是move

2. cp

> copy

3. rm   
-r 递归删除 (也就是删除目录和目录下所有文件)   
-d 删除目录.    
-v 显示过程(view,这是统一的)   
-f 强制执行.  
-- 后接一个字符,然后删除以对应字符(作为名字)开头的文件.
> remove    
*三者和C语言的一些函数的参数使用方式:*
*差异性: 这些有多余的-参数, 并且这个是"操作对象, 目标"的操作顺序.*   
*统一性: 都有两大基本操作对象(和strcpy类似, 只是参数顺序不同而已)*

#### 8.GPT MBR 多重引导

gpt是GUID partion table 是更高级的分区方式 (可能使用大概2M  BIOS boot来保存更多的系统启动代码)

MBR是一种普通的分区方式, 无法支持更多的存储

> 两者之间 差异化: MBR只有一块记录分区信息的table(和MBR被共同存储在第一个扇区, 而GPT有多块(第一块LBA和MBR类似,**但是原本的分区表被分散到后面去了**,存在多个LBA, 每个LBA都能存储四个分区信息)  
> 统一化: 通过"分区表"和"启动程序码"来实现功能

多重引导是通过bootloader 

> 每个分区可以拥有自己的"开机扇区 boot sector"(类似于MBR区或者LBA0的东西)
> 这是实现多重引导的原因.

#### 9.命令 scp :

secure copy , 除了在本机拷贝, 还支持跨服务器拷贝.

用法: scp 操作对象 目标对象

其中, 远程对象必须以(username@)ip: filename的格式表示

>另外有一些常用参数: -v (view)  
-r  (recursion) 
-C  (compress)      
-1  强制scp命令使用协议ssh1  
-2  强制scp命令使用协议ssh2  
-4  强制scp命令只使用IPv4寻址  
-6  强制scp命令只使用IPv6寻址  
>> 这和一些"其他命令的参数"以及"命令行中命令提示"    
>> 差异化: 就是一些独特命令(比如IPv网络命令不同)   
>> 统一化: 
>> 1. 比如-r -v;
>> 2. 比如所有参数, 摆放位置(这和C语言也正好有对立部分)
>> 3. 比如 @的作用: 也是user @ machine

#### 10. ps     
常用:   
-A : 显示所有程序   
e : 显示所有程序及其环境变量     
-f : 显示所有程序及其依赖关系(通过树状图展示)   
#### 11. cat   
主要作用是*打印文本内容*和*连接文本*:   
1. 打印文本内容:     
有一些常用命令选项:     
> 1. -n打印时附上行号   
> 2. -s消去多余空行(将多行空行换成一行)     
> 3. 其它   
2. 连接文本(重定向机制,注意重定向如果缺少对象, 则代表标准输入/输出):    
> 1. \> 和strcpy类似
> 2. \>> 追加和strcat类似    
>> 两者和str函数的差异性: str函数并不具有新建的功能.而重定向具有  
>> 统一性: 基本统一.    
#### 12. top:   
1. 交互式命令:  
k: 终止一个进程     
q: 退出top程序  
h: help     
s: 改变刷新间隔     
c: 切换显示命令名称和完整命令行    
M: 根据内存大小进行排序     
P: 根据CPU百分率排序    
T: 根据时间进行排序     
W: 将当前设置写入~/.toprc当中(用户配置文件)    
> 内部之间的差异: 模式切换多为**大写**,其它多为**小写*  
> 内部之间的统一: 和动作的英文单词相统一,k,q,h,s(可能表示second吧),c(command_line) M(Memory_mode) ... W比较特殊.    
#### 13. ps 
常用参数选项:   
-A 显示所有进程
-a 显示所有终端的进程   
#### 14. echo(回声)

作用就是打印变量    

#### 15. ls

-a 打印所有文件,目录    
-l 以行列表形式打印     
-F 用斜杠标识目录

> `ll` 的效果和 ls -alF相同.   

#### 16.pwd     
获取当前目录绝对路径.   
#### 17.netstat
常用选项:   
-c 持续打印     
-t tcp协议套接字
-u udp协议套接字    
> tcp 和 udp之间的关系,就好像"轨道交通"和"公路交通"的关系.

-n 禁止域名解析, 加快显示.   
-

#### 18.more 和 less    
查看文本文件    
空格翻页(more,less)  
上下左右(less)  
> less实现了更慢,精细的文本翻页浏览.

#### 19.