note
====

进程的状态信息和控制信息等由proc 和 user 结构体控制。
每个进程都会分配一组上述结构体的实例。
proc常驻内存，而user可能被换出。

proc存放着每个进程的状态、优先级等与进程相关的信息。proc的长度就是系统进程个数的限制数。长度由NPROC控制。
user结构体用来管理进程打开的文件或目录的信息。内核只需要当前执行进程的结构体，所以进程被换出时，相应的结构体就没用了。而proc还存在是因为需要进行进程调度。

内核可以通过全局变量u来访问user结构体。

为进程分配内存：
    代码段和数据段作为连续的物理区域分配给进程。进程通过虚拟地址访问被分配的内存物理内存区域。（有可能不是连续的，因为代码段只读。多个相同进程的代码段可以共享同一个。）（虚拟地址连续？）
    数据段的物理地址长度由proc.p_adr 和 proc.p_size 控制。

    数据段前面存放着user结构体和内核栈区域，作为内核临时用。长度为1kb

内核把编号为6的PAR设置为执行进程的数据段的物理地址，所以可以通过u(0140000)访问user结构体。


------


fork的时候，子进程会复制父进程各种信息。然后处理好父子的相关变量。数据段和PPDA都会复制。因为子进程继承了父进程已打开的文件和目录信息。代码段不复制，共享即可。

多个进程是否共用代码段看程序的魔术数字。

-------

swap换入的时候，代码段读入内存中，swap中的代码段不删除，因为代码段只读，不会变化，所以可以这样优化

sched()被proc[0]定期调用，寻找可以被换出的对象


--------
信号是一种进程间互相通信的机制。

信号可以实现：1.剥夺用户进程的控制权  2.终止用户进程的运行  3.跟踪用户的处理

unix v6 通过给user.u_signal[n] 赋值实现自定义的信号处理函数。赋值0表示停止进程，奇数表示忽略，偶数表示处理相应的处理函数。


内核转储core()?


