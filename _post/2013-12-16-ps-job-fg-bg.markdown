---
layout: post
title: 进程相关命令
categories:
- TOOL
---

ps参数说明：

	-a	显示所有终端机下执行的进程，除了阶段作业领导者之外。
	a	显示现行终端机下的所有进程，包括其他用户的进程。**
	-A	显示所有进程。
	-c	显示CLS和PRI栏位。
	c	列出进程时，显示每个进程真正的指令名称，而不包含路径，参数或常驻服务的标示。
	-C<指令名称> 　指定执行指令的名称，并列出该指令的进程的状况。
	-d 　	显示所有进程，但不包括阶段作业领导者的进程。
	-e 　	此参数的效果和指定"A"参数相同。**
	e 　	列出进程时，显示每个进程所使用的环境变量。
	-f 　	显示UID,PPIP,C与STIME栏位。
	**f 　	用ASCII字符显示树状结构，表达进程间的相互关系。**
	-g<群组名称> 　此参数的效果和指定"-G"参数相同，当亦能使用阶段作业领导者的名称来指定。
	g 　	显示现行终端机下的所有进程，包括群组领导者的进程。
	-G<群组识别码> 　列出属于该群组的进程的状况，也可使用群组名称来指定。
	h 　	不显示标题列。
	-H 　	显示树状结构，表示进程间的相互关系。
	-j或j 　	采用工作控制的格式显示进程状况。
	-l或l 采用详细的格式来显示进程状况。**
	L 　	列出栏位的相关信息。
	-m或m 　显示所有的执行绪。
	n 　	以数字来表示USER和WCHAN栏位。
	-N 　	显示所有的进程，除了执行ps指令终端机下的进程之外。
	-p<进程识别码> 　指定进程识别码，并列出该进程的状况。
	p<进程识别码> 　	此参数的效果和指定"-p"参数相同，只在列表格式方面稍有差异。
	r 　	只列出现行终端机正在执行中的进程。
	-s<阶段作业> 　	指定阶段作业的进程识别码，并列出隶属该阶段作业的进程的状况。
	s 　	采用进程信号的格式显示进程状况。
	S 　	列出进程时，包括已中断的子进程资料。
	-t<终端机编号> 　指定终端机编号，并列出属于该终端机的进程的状况。
	t<终端机编号> 　	此参数的效果和指定"-t"参数相同，只在列表格式方面稍有差异。
	-T 　	显示现行终端机下的所有进程。
	-u<用户识别码> 　此参数的效果和指定"-U"参数相同。
	u 　	以用户为主的格式来显示进程状况。**
	-U<用户识别码> 　列出属于该用户的进程的状况，也可使用用户名称来指定。
	U<用户名称> 　	列出属于该用户的进程的状况。
	v 　	采用虚拟内存的格式显示进程状况。
	-V或V 　显示版本信息。
	-w或w 　采用宽阔的格式来显示进程状况。
	x 　	显示所有进程，不以终端机来区分。**
	X 　	采用旧式的Linux i386登陆格式显示进程状况。
	-y	配合参数"-l"使用时，不显示F(flag)栏位，并以RSS栏位取代ADDR栏位


常用格式
    
    ps aue
    ps -elf

	%CPU:进程占用CPU的百分比
	%MEM:占用内存百分比
	VSZ: 进程虚拟大小
	RSS:驻留中页的数量
	TTY: 终端ID
	STAT: 进程状态
	START:启动进程的时间
	TIME: 进程消耗CPU时间
	COMMAND:进程名称和参数

======================================================================

STAT对应的进程状态

	D:不可打断的休眠状态，通常是IO状态
	R:正在运行中在队列中可过行的
	S:处于休眠状态
	T:停止或被追踪
	W:进入内存交换
	X:死掉的进程
	Z:僵死进程
	<:优先级高的进程
	N:优先级低的进程
	L:有些页被锁进进程
	s:进程的领导者(在它之下有子进程)
	l:多进程进程
	+:处于后台的进程

======================================================================

要想要一个命令在后台运行可以在命令后加上'&'符号

例如:
    
    find / -name sed笔记 2>/dev/null&
    [root@localhost shell]# top&
    [1] 5681

前台进程可以与后台进程进行转换:

前台转后台的方法是在程序运行时使用Ctrl+Z，这个快捷键会将当前进程挂起；

当进程被挂起时就相当与暂停了进程的运行;使用bg命令刚刚被挂起的进程再次运行，不过它是在后台运行了，而不是在前台;

后台转换为前台：

如果进程在后台运行，则使用fg命令就将后台进程转到前台

多个后台进程的调度:

当有多个后台进程时候调度指定进程到前台

    
    [root@localhost shell]# jobs
    [1]   Stopped                 vim
    [2]-  Stopped                 top
    [3]+  Stopped                 top
    
    [root@localhost shell]# jobs -l
    [1]   5765 停止                vim
    [2]-  5766 停止 (信号)         top
    [3]+  5767 停止 (信号)         top
    [root@localhost shell]# bg %1
    [1] vim &


如果系统中有多个后台进程，那么shell会标志当前进程和前一个进程。

fg命令会将当前进程带到前台，而bg命令会将当前进程回复到后台执行；

jobs命令就是用来判断所有被挂起(停止)的进程、后台进程的作业号，以及哪个是当前进程(+)，前一个进程(-)

======================================================================

jobs

用途:显示当前会话作业的状态

jobs [-l|-n|-p] [JobID]
	-l纤细详细的作业信息，包括作业号、当前作业、进程组标志、状态和启动作业的命令
	-p显示了所选定的作业的进程组引导符的进程标识,如果指明-p选项则只输出进程标志
	-n显示从最后一次通知后停止或退出的作业
    
    [root@localhost shell]# jobs -l
    [1]+  5765 Stoped      vim
    [2]   5766 Stoped      top
    [3]-  5767 Stoped      top

其中[1]代表进程组号

+或-分别指明了当前进程和前一个进程

如果当前进程退出就用一个'-'(减号标志)来标志将要成为默认作业的作业。

这个作业也能够用%+和%%来指定。

state显示一下值之一
	Running 表示作业没有被信号挂起并没有退出
	Done 表示作业已完成，并返回退出状态0
	Stoped 表示挂起状态

======================================================================

fg
作用:在前台运行作业
语法:fg [JobID]

fg命令移动当前环境中的后台作业到前台来，使用JobID参数指明在前台下要运行的特定作业。如果没有提供参数，则默认使用最近在后台被挂起的作业

JobID参数可以是进程的标识号，也可以使用如下组合:

	%Number 通过作业编号引用作业
	%String 引用名称以特定字符串开头的作业
	%?String 引用名称中包含特地字符串的作业
	%+OR%% 引用当前作业，%-引用前一个作业

======================================================================

bg

作用:在后台运行作业

语法:bg [JobID]

bg命令移动当前环境中的后台作业到前台来，使用JobID参数指明在前台下要运行的特定作业。如果没有提供参数，则默认使用最近在后台被挂起的作业

JobID参数可以是进程的标识号，也可以使用如下组合:

	%Number 通过作业编号引用作业
	%String 引用名称以特定字符串开头的作业
	%?String 引用名称中包含特地字符串的作业
	%+OR%% 引用当前作业，%-引用前一个作业

##### 注意:
作业号可以与wait、fg、kill共同使用，只要在作业号前加入%前缀；

例如:	
	kill -9 %3

使用Ctrl+C挂起作业，使用bg命令就可以在后台重启作业。

当作业无需终端输入且作业输出被重定向至非终端文件时，这么做是有效的。

如果后台作业具有终端输出，可以输入一下命令强制停止该作业

======================================================================
