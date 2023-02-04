Linux ps 顯示的 stat 簡介
====
参考来源资讯 : https://unix.stackexchange.com/questions/18474/what-does-this-process-stat-indicates
<details>
<summary>介紹</summary>
状态

D (uninterruptible sleep) - 在不可中断的休眠中 (一般为正在进行输入/输出) 通常是 IO

R (running) - 在运行中或可以被运行 (即在运行序列 run queue)

S (sleeping) - 在可以被中断的休眠中 (一般是正在等待某事件完结)

T (traced or stopped) - 已被停止。因工作控制讯号 (job control signal) 或Process在被追踪中。

Z (Zombie) - 不能运作的进程，即所谓僵尸进程。一般因为已终止但未能被其母进程成功接收的进程。


附加的选项

<高优先级（对其他用户不利）

N低优先级（对其他用户很好）

L已将页面锁定在内存中（用于实时和自定义IO）

s是会议负责人

l是多线程的（使用CLONE_THREAD，就像NPTL pthreads一样）

+在前台进程组中


例子

登入 : Ss   sshd: ryanchen9 [priv]

       S    sshd: ryanchen9@pts/2

执行查看指令 : R+   ps -e -o stat,command,pid


其他 : 

S<l  /usr/bin/pulseaudio --start   

Ss   oracletopprd (LOCAL=NO)

Ssl  /usr/libexec/upowerd
</details>
<details>
<summary>排序</summary>
預設是從小開始

—sort= 指令加 - 會反向 

原本 —sort ( 0 , 1 , 2 ... ) 
反向 —sort=- ( 99 , 98 ... )

系統上最耗費記憶體的程式
ps -eo pid,ppid,cmd,%mem,%cpu --sort=-%mem | head

這行指令可利用 ps 指令列出行程的一些基本資訊，
按照每個行程所使用的記憶體排序後，列出排名最前面的幾個行程
</details>
