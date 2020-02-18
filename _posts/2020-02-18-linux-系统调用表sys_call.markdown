---
layout: post
title:  "linux-系统调用表sys_call"
tags: linux
---

### 概览 (IO, 内存， 进程)

![SystemCallInterface](../../../images/postimg/SCI_system_call_interface.png)


IBM网站

[https://www.ibm.com/developerworks/cn/linux/kernel/syscall/part1/appendix.html](https://www.ibm.com/developerworks/cn/linux/kernel/syscall/part1/appendix.html "https://www.ibm.com/developerworks/cn/linux/kernel/syscall/part1/appendix.html")


<h2 style="font-weight: normal;">Linux系统调用表1 （附linux源码）</h2>

<div id="content_views" class="markdown_views prism-atom-one-dark">
<svg xmlns="http://www.w3.org/2000/svg" style="display: none;">
    <path stroke-linecap="round" d="M5,0 0,2.5 5,5z" id="raphael-marker-block" style="-webkit-tap-highlight-color: rgba(0, 0, 0, 0);"></path>
</svg>
<h3 id="一进程控制"><a name="t0"></a><a name="t0"></a>一、进程控制：</h3>

<div class="table-box"><table>
<thead>
<tr>
  <th align="left">函数名</th>
  <th align="left">描述</th>
  <th align="left">文件</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">fork</td>
  <td align="left">创建一个新进程</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/fork.c" rel="nofollow" target="_blank">kernel/fork.c</a></td>
</tr>
<tr>
  <td align="left">clone</td>
  <td align="left">按指定条件创建子进程</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/fork.c" rel="nofollow" target="_blank">kernel/fork.c</a></td>
</tr>
<tr>
  <td align="left">execve</td>
  <td align="left">运行可执行文件</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/exec.c" rel="nofollow" target="_blank">fs/exec.c</a></td>
</tr>
<tr>
  <td align="left">exit</td>
  <td align="left">中止进程</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/exit.c" rel="nofollow" target="_blank">kernel/exit.c</a></td>
</tr>
<tr>
  <td align="left">_exit</td>
  <td align="left">立即中止当前进程</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">getdtablesize</td>
  <td align="left">进程所能打开的最大文件数</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getpgid</td>
  <td align="left">获取指定进程组标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setpgid</td>
  <td align="left">设置指定进程组标志号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getpgrp</td>
  <td align="left">获取当前进程组标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setpgrp</td>
  <td align="left">设置当前进程组标志号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getpid</td>
  <td align="left">获取进程标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getppid</td>
  <td align="left">获取父进程标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getpriority</td>
  <td align="left">获取调度优先级</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setpriority</td>
  <td align="left">设置调度优先级</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">modify_ldt</td>
  <td align="left">读写进程的本地描述表</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/um/ldt.c" rel="nofollow" target="_blank">arch/x86/um/ldt.c</a></td>
</tr>
<tr>
  <td align="left">nanosleep</td>
  <td align="left">使进程睡眠指定的时间</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/hrtimer.c" rel="nofollow" target="_blank">kernel/hrtimer.c</a></td>
</tr>
<tr>
  <td align="left">nice</td>
  <td align="left">改变分时进程的优先级</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">pause</td>
  <td align="left">挂起进程，等待信号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow" target="_blank">kernel/signal.c</a></td>
</tr>
<tr>
  <td align="left">personality</td>
  <td align="left">设置进程运行域</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/exec_domain.c" rel="nofollow" target="_blank">kernel/exec_domain.c</a></td>
</tr>
<tr>
  <td align="left">prctl</td>
  <td align="left">对进程进行特定操作</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">ptrace</td>
  <td align="left">进程跟踪</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/ptrace.c" rel="nofollow" target="_blank">kernel/ptrace.c</a></td>
</tr>
<tr>
  <td align="left">sched_get_priority_max</td>
  <td align="left">取得静态优先级的上限</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow" target="_blank">kernel/sched/core.c</a></td>
</tr>
<tr>
  <td align="left">sched_get_priority_min</td>
  <td align="left">取得静态优先级的下限</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow" target="_blank">kernel/sched/core.c</a></td>
</tr>
<tr>
  <td align="left">sched_getparam</td>
  <td align="left">取得进程的调度参数</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow" target="_blank">kernel/sched/core.c</a></td>
</tr>
<tr>
  <td align="left">sched_getscheduler</td>
  <td align="left">取得指定进程的调度策略</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow" target="_blank">kernel/sched/core.c</a></td>
</tr>
<tr>
  <td align="left">sched_rr_get_interval</td>
  <td align="left">取得按RR算法调度的实时进程的时间片长度</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow" target="_blank">kernel/sched/core.c</a></td>
</tr>
<tr>
  <td align="left">sched_setparam</td>
  <td align="left">设置进程的调度参数</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow" target="_blank">kernel/sched/core.c</a></td>
</tr>
<tr>
  <td align="left">sched_setscheduler</td>
  <td align="left">设置指定进程的调度策略和参数</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow" target="_blank">kernel/sched/core.c</a></td>
</tr>
<tr>
  <td align="left">sched_yield</td>
  <td align="left">进程主动让出处理器,并将自己等候调度队列队尾</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow" target="_blank">kernel/sched/core.c</a></td>
</tr>
<tr>
  <td align="left">vfork</td>
  <td align="left">创建一个子进程，以供执行新程序，常与execve等同时使用</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/fork.c" rel="nofollow" target="_blank">kernel/fork.c</a></td>
</tr>
<tr>
  <td align="left">wait</td>
  <td align="left">等待子进程终止</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">wait3</td>
  <td align="left">参见wait</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">waitpid</td>
  <td align="left">等待指定子进程终止</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">wait4</td>
  <td align="left">参见waitpid</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/exit.c" rel="nofollow" target="_blank">kernel/exit.c</a></td>
</tr>
<tr>
  <td align="left">capget</td>
  <td align="left">获取进程权限</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/capability.c" rel="nofollow" target="_blank">kernel/capability.c</a></td>
</tr>
<tr>
  <td align="left">capset</td>
  <td align="left">设置进程权限</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/capability.c" rel="nofollow" target="_blank">kernel/capability.c</a></td>
</tr>
<tr>
  <td align="left">getsid</td>
  <td align="left">获取会晤标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setsid</td>
  <td align="left">设置会晤标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
</tbody></table></div>


<hr>

<h3 id="二文件系统控制"><a name="t1"></a><a name="t1"></a>二、文件系统控制</h3>

<div class="table-box"><table>
<thead>
<tr>
  <th align="left">函数名</th>
  <th align="left">描述</th>
  <th align="left">文件</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">fcntl</td>
  <td align="left">文件控制</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/fcntl.c" rel="nofollow" target="_blank">fs/fcntl.c</a></td>
</tr>
<tr>
  <td align="left">open</td>
  <td align="left">打开文件</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">creat</td>
  <td align="left">创建新文件</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">close</td>
  <td align="left">关闭文件描述字</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">read</td>
  <td align="left">读文件</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow" target="_blank">fs/read_write.c</a></td>
</tr>
<tr>
  <td align="left">write</td>
  <td align="left">写文件</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow" target="_blank">fs/read_write.c</a></td>
</tr>
<tr>
  <td align="left">readv</td>
  <td align="left">从文件读入数据到缓冲数组中</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow" target="_blank">fs/read_write.c</a></td>
</tr>
<tr>
  <td align="left">writev</td>
  <td align="left">将缓冲数组里的数据写入文件</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow" target="_blank">fs/read_write.c</a></td>
</tr>
<tr>
  <td align="left">pread</td>
  <td align="left">对文件随机读</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow" target="_blank">fs/read_write.c</a></td>
</tr>
<tr>
  <td align="left">pwrite</td>
  <td align="left">对文件随机写</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow" target="_blank">fs/read_write.c</a></td>
</tr>
<tr>
  <td align="left">lseek</td>
  <td align="left">移动文件指针</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow" target="_blank">fs/read_write.c</a></td>
</tr>
<tr>
  <td align="left">_llseek</td>
  <td align="left">在64位地址空间里移动文件指针</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">dup</td>
  <td align="left">复制已打开的文件描述字</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/file.c" rel="nofollow" target="_blank">fs/file.c</a></td>
</tr>
<tr>
  <td align="left">dup2</td>
  <td align="left">按指定条件复制文件描述字</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/file.c" rel="nofollow" target="_blank">fs/file.c</a></td>
</tr>
<tr>
  <td align="left">flock</td>
  <td align="left">文件加/解锁</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/locks.c" rel="nofollow" target="_blank">fs/locks.c</a></td>
</tr>
<tr>
  <td align="left">poll</td>
  <td align="left">I/O多路转换</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/select.c" rel="nofollow" target="_blank">fs/select.c</a></td>
</tr>
<tr>
  <td align="left">truncate</td>
  <td align="left">截断文件</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">ftruncate</td>
  <td align="left">参见truncate</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">umask</td>
  <td align="left">设置文件权限掩码</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">fsync</td>
  <td align="left">把文件在内存中的部分写回磁盘</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/sync.c" rel="nofollow" target="_blank">fs/sync.c</a></td>
</tr>
<tr>
  <td align="left">access</td>
  <td align="left">确定文件的可存取性</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">chdir</td>
  <td align="left">改变当前工作目录</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">fchdir</td>
  <td align="left">参见chdir</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">chmod</td>
  <td align="left">改变文件方式</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">fchmod</td>
  <td align="left">参见chmod</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">chown</td>
  <td align="left">改变文件的属主或用户组</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">fchown</td>
  <td align="left">参见chown</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">lchown</td>
  <td align="left">参见chown</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">chroot</td>
  <td align="left">改变根目录</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">stat</td>
  <td align="left">取文件状态信息</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/stat.c" rel="nofollow" target="_blank">fs/stat.c</a></td>
</tr>
<tr>
  <td align="left">lstat</td>
  <td align="left">参见stat</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/stat.c" rel="nofollow" target="_blank">fs/stat.c</a></td>
</tr>
<tr>
  <td align="left">fstat</td>
  <td align="left">参见stat</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/stat.c" rel="nofollow" target="_blank">fs/stat.c</a></td>
</tr>
<tr>
  <td align="left">statfs</td>
  <td align="left">取文件系统信息</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/statfs.c" rel="nofollow" target="_blank">fs/statfs.c</a></td>
</tr>
<tr>
  <td align="left">fstatfs</td>
  <td align="left">参见statfs</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/statfs.c" rel="nofollow" target="_blank">fs/statfs.c</a></td>
</tr>
<tr>
  <td align="left">readdir</td>
  <td align="left">读取目录项</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">getdents</td>
  <td align="left">读取目录项</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/readdir.c" rel="nofollow" target="_blank">fs/readdir.c</a></td>
</tr>
<tr>
  <td align="left">mkdir</td>
  <td align="left">创建目录</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow" target="_blank">fs/namei.c</a></td>
</tr>
<tr>
  <td align="left">mknod</td>
  <td align="left">创建索引节点</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow" target="_blank">fs/namei.c</a></td>
</tr>
<tr>
  <td align="left">rmdir</td>
  <td align="left">删除目录</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow" target="_blank">fs/namei.c</a></td>
</tr>
<tr>
  <td align="left">rename</td>
  <td align="left">文件改名</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow" target="_blank">fs/namei.c</a></td>
</tr>
<tr>
  <td align="left">link</td>
  <td align="left">创建链接</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow" target="_blank">fs/namei.c</a></td>
</tr>
<tr>
  <td align="left">symlink</td>
  <td align="left">创建符号链接</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow" target="_blank">fs/namei.c</a></td>
</tr>
<tr>
  <td align="left">unlink</td>
  <td align="left">删除链接</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow" target="_blank">fs/namei.c</a></td>
</tr>
<tr>
  <td align="left">readlink</td>
  <td align="left">读符号链接的值</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/stat.c" rel="nofollow" target="_blank">fs/stat.c</a></td>
</tr>
<tr>
  <td align="left">mount</td>
  <td align="left">安装文件系统</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namespace.c" rel="nofollow" target="_blank">fs/namespace.c</a></td>
</tr>
<tr>
  <td align="left">umount</td>
  <td align="left">卸下文件系统</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">ustat</td>
  <td align="left">取文件系统信息</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/statfs.c" rel="nofollow" target="_blank">fs/statfs.c</a></td>
</tr>
<tr>
  <td align="left">utime</td>
  <td align="left">改变文件的访问修改时间</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/utimes.c" rel="nofollow" target="_blank">fs/utimes.c</a></td>
</tr>
<tr>
  <td align="left">utimes</td>
  <td align="left">参见utime</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/utimes.c" rel="nofollow" target="_blank">fs/utimes.c</a></td>
</tr>
<tr>
  <td align="left">quotactl</td>
  <td align="left">控制磁盘配额</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/quota/quota.c" rel="nofollow" target="_blank">fs/quota/quota.c</a></td>
</tr>
</tbody></table></div>


<hr>

<h3 id="三系统控制"><a name="t2"></a><a name="t2"></a>三、系统控制</h3>

<div class="table-box"><table>
<thead>
<tr>
  <th align="left">函数名</th>
  <th align="left">描述</th>
  <th align="left">文件</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">ioctl</td>
  <td align="left">I/O总控制函数</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/ioctl.c" rel="nofollow" target="_blank">fs/ioctl.c</a></td>
</tr>
<tr>
  <td align="left">_sysctl</td>
  <td align="left">读/写系统参数</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sysctl_binary.c" rel="nofollow" target="_blank">kernel/sysctl_binary.c</a></td>
</tr>
<tr>
  <td align="left">acct</td>
  <td align="left">启用或禁止进程记账</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/acct.c" rel="nofollow" target="_blank">kernel/acct.c</a></td>
</tr>
<tr>
  <td align="left">getrlimit</td>
  <td align="left">获取系统资源上限</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setrlimit</td>
  <td align="left">设置系统资源上限</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getrusage</td>
  <td align="left">获取系统资源使用情况</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">uselib</td>
  <td align="left">选择要使用的二进制函数库</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/exec.c" rel="nofollow" target="_blank">fs/exec.c</a></td>
</tr>
<tr>
  <td align="left">ioperm</td>
  <td align="left">设置端口I/O权限</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/kernel/ioport.c" rel="nofollow" target="_blank">arch/x86/kernel/ioport.c</a></td>
</tr>
<tr>
  <td align="left">iopl</td>
  <td align="left">改变进程I/O权限级别</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/kernel/ioport.c" rel="nofollow" target="_blank">arch/x86/kernel/ioport.c</a></td>
</tr>
<tr>
  <td align="left">outb</td>
  <td align="left">低级端口操作</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">reboot</td>
  <td align="left">重新启动</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/reboot.c" rel="nofollow" target="_blank">kernel/reboot.c</a></td>
</tr>
<tr>
  <td align="left">swapon</td>
  <td align="left">打开交换文件和设备</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/swapfile.c" rel="nofollow" target="_blank">mm/swapfile.c</a></td>
</tr>
<tr>
  <td align="left">swapoff</td>
  <td align="left">关闭交换文件和设备</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/swapfile.c" rel="nofollow" target="_blank">mm/swapfile.c</a></td>
</tr>
<tr>
  <td align="left">bdflush</td>
  <td align="left">控制bdflush守护进程</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sysfs</td>
  <td align="left">取核心支持的文件系统类型</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/filesystems.c" rel="nofollow" target="_blank">fs/filesystems.c</a></td>
</tr>
<tr>
  <td align="left">sysinfo</td>
  <td align="left">取得系统信息</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">adjtimex</td>
  <td align="left">调整系统时钟</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/time.c" rel="nofollow" target="_blank">kernel/time.c</a></td>
</tr>
<tr>
  <td align="left">alarm</td>
  <td align="left">设置进程的闹钟</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/timer.c" rel="nofollow" target="_blank">kernel/timer.c</a></td>
</tr>
<tr>
  <td align="left">getitimer</td>
  <td align="left">获取计时器值</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/itimer.c" rel="nofollow" target="_blank">kernel/itimer.c</a></td>
</tr>
<tr>
  <td align="left">setitimer</td>
  <td align="left">设置计时器值</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/itimer.c" rel="nofollow" target="_blank">kernel/itimer.c</a></td>
</tr>
<tr>
  <td align="left">gettimeofday</td>
  <td align="left">取时间和时区</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/time.c" rel="nofollow" target="_blank">kernel/time.c</a></td>
</tr>
<tr>
  <td align="left">settimeofday</td>
  <td align="left">设置时间和时区</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/time.c" rel="nofollow" target="_blank">kernel/time.c</a></td>
</tr>
<tr>
  <td align="left">stime</td>
  <td align="left">设置系统日期和时间</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">time</td>
  <td align="left">取得系统时间</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">times</td>
  <td align="left">取进程运行时间</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">uname</td>
  <td align="left">获取当前UNIX系统的名称、版本和主机等信息</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">vhangup</td>
  <td align="left">挂起当前终端</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow" target="_blank">fs/open.c</a></td>
</tr>
<tr>
  <td align="left">nfsservctl</td>
  <td align="left">对NFS守护进程进行控制</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">vm86</td>
  <td align="left">进入模拟8086模式</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">create_module</td>
  <td align="left">创建可装载的模块项</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">delete_module</td>
  <td align="left">删除可装载的模块项</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/module.c" rel="nofollow" target="_blank">kernel/module.c</a></td>
</tr>
<tr>
  <td align="left">init_module</td>
  <td align="left">初始化模块</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/module.c" rel="nofollow" target="_blank">kernel/module.c</a></td>
</tr>
<tr>
  <td align="left">query_module</td>
  <td align="left">查询模块信息</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">*get_kernel_syms</td>
  <td align="left">取得核心符号,已被query_module代替</td>
  <td align="left"></td>
</tr>
</tbody></table></div>


<hr>

<h3 id="四内存管理"><a name="t3"></a><a name="t3"></a>四、内存管理</h3>

<div class="table-box"><table>
<thead>
<tr>
  <th align="left">函数名</th>
  <th align="left">描述</th>
  <th align="left">文件</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">brk</td>
  <td align="left">改变数据段空间的分配</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mmap.c" rel="nofollow" target="_blank">mm/mmap.c</a></td>
</tr>
<tr>
  <td align="left">sbrk</td>
  <td align="left">参见brk</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">mlock</td>
  <td align="left">内存页面加锁</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mlock.c" rel="nofollow" target="_blank">mm/mlock.c</a></td>
</tr>
<tr>
  <td align="left">munlock</td>
  <td align="left">内存页面解锁</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mlock.c" rel="nofollow" target="_blank">mm/mlock.c</a></td>
</tr>
<tr>
  <td align="left">mlockall</td>
  <td align="left">调用进程所有内存页面加锁</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mlock.c" rel="nofollow" target="_blank">mm/mlock.c</a></td>
</tr>
<tr>
  <td align="left">munlockall</td>
  <td align="left">调用进程所有内存页面解锁</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mlock.c" rel="nofollow" target="_blank">mm/mlock.c</a></td>
</tr>
<tr>
  <td align="left">mmap</td>
  <td align="left">映射虚拟内存页</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/kernel/sys_x86_64.c" rel="nofollow" target="_blank">arch/x86/kernel/sys_x86_64.c</a></td>
</tr>
<tr>
  <td align="left">munmap</td>
  <td align="left">去除内存页映射</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mmap.c" rel="nofollow" target="_blank">mm/mmap.c</a></td>
</tr>
<tr>
  <td align="left">mremap</td>
  <td align="left">重新映射虚拟内存地址</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mmap.c" rel="nofollow" target="_blank">mm/mmap.c</a></td>
</tr>
<tr>
  <td align="left">msync</td>
  <td align="left">将映射内存中的数据写回磁盘</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/msync.c" rel="nofollow" target="_blank">mm/msync.c</a></td>
</tr>
<tr>
  <td align="left">mprotect</td>
  <td align="left">设置内存映像保护</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mprotect.c" rel="nofollow" target="_blank">mm/mprotect.c</a></td>
</tr>
<tr>
  <td align="left">getpagesize</td>
  <td align="left">获取页面大小</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sync</td>
  <td align="left">将内存缓冲区数据写回硬盘</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/sync.c" rel="nofollow" target="_blank">fs/sync.c</a></td>
</tr>
<tr>
  <td align="left">cacheflush</td>
  <td align="left">将指定缓冲区中的内容写回磁盘</td>
  <td align="left"></td>
</tr>
</tbody></table></div>


<hr>

<h3 id="五网络管理"><a name="t4"></a><a name="t4"></a>五、网络管理</h3>

<div class="table-box"><table>
<thead>
<tr>
  <th align="left">函数名</th>
  <th align="left">描述</th>
  <th align="left">文件</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">getdomainname</td>
  <td align="left">取域名</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">setdomainname</td>
  <td align="left">设置域名</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">gethostid</td>
  <td align="left">获取主机标识号</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sethostid</td>
  <td align="left">设置主机标识号</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">gethostname</td>
  <td align="left">获取本主机名称</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sethostname</td>
  <td align="left">设置主机名称</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
</tbody></table></div>


<hr>

<h3 id="六socket控制"><a name="t5"></a><a name="t5"></a>六、socket控制</h3>

<div class="table-box"><table>
<thead>
<tr>
  <th align="left">函数名</th>
  <th align="left">描述</th>
  <th align="left">文件</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">socketcall</td>
  <td align="left">socket系统调用</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">socket</td>
  <td align="left">建立socket</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">bind</td>
  <td align="left">绑定socket到端口</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">connect</td>
  <td align="left">连接远程主机</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">accept</td>
  <td align="left">响应socket连接请求</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">send</td>
  <td align="left">通过socket发送信息</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sendto</td>
  <td align="left">发送UDP信息</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">sendmsg</td>
  <td align="left">参见send</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">recv</td>
  <td align="left">通过socket接收信息</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">recvfrom</td>
  <td align="left">接收UDP信息</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">recvmsg</td>
  <td align="left">参见recv</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">listen</td>
  <td align="left">监听socket端口</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">select</td>
  <td align="left">对多路同步I/O进行轮询</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/select.c" rel="nofollow" target="_blank">fs/select.c</a></td>
</tr>
<tr>
  <td align="left">shutdown</td>
  <td align="left">关闭socket上的连接</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">getsockname</td>
  <td align="left">取得本地socket名字</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">getpeername</td>
  <td align="left">获取通信对方的socket名字</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">getsockopt</td>
  <td align="left">取端口设置</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">setsockopt</td>
  <td align="left">设置端口参数</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
<tr>
  <td align="left">sendfile</td>
  <td align="left">在文件或端口间传输数据</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow" target="_blank">fs/read_write.c</a></td>
</tr>
<tr>
  <td align="left">socketpair</td>
  <td align="left">创建一对已联接的无名socket</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow" target="_blank">net/socket.c</a></td>
</tr>
</tbody></table></div>


<hr>

<h3 id="七用户管理"><a name="t6"></a><a name="t6"></a>七、用户管理</h3>

<div class="table-box"><table>
<thead>
<tr>
  <th align="left">函数名</th>
  <th align="left">描述</th>
  <th align="left">文件</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">getuid</td>
  <td align="left">获取用户标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setuid</td>
  <td align="left">设置用户标志号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getgid</td>
  <td align="left">获取组标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setgid</td>
  <td align="left">设置组标志号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getegid</td>
  <td align="left">获取有效组标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setegid</td>
  <td align="left">设置有效组标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">geteuid</td>
  <td align="left">获取有效用户标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">seteuid</td>
  <td align="left">设置有效用户标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setregid</td>
  <td align="left">分别设置真实和有效的的组标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setreuid</td>
  <td align="left">分别设置真实和有效的用户标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getresgid</td>
  <td align="left">分别获取真实的,有效的和保存过的组标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setresgid</td>
  <td align="left">分别设置真实的,有效的和保存过的组标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getresuid</td>
  <td align="left">分别获取真实的,有效的和保存过的用户标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setresuid</td>
  <td align="left">分别设置真实的,有效的和保存过的用户标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setfsgid</td>
  <td align="left">设置文件系统检查时使用的组标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">setfsuid</td>
  <td align="left">设置文件系统检查时使用的用户标识号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow" target="_blank">kernel/sys.c</a></td>
</tr>
<tr>
  <td align="left">getgroups</td>
  <td align="left">获取后补组标志清单</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/groups.c" rel="nofollow" target="_blank">kernel/groups.c</a></td>
</tr>
<tr>
  <td align="left">setgroups</td>
  <td align="left">设置后补组标志清单</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/groups.c" rel="nofollow" target="_blank">kernel/groups.c</a></td>
</tr>
</tbody></table></div>


<hr>

<h3 id="八进程间通信"><a name="t7"></a><a name="t7"></a>八、进程间通信</h3>

<div class="table-box"><table>
<thead>
<tr>
  <th align="left">函数名</th>
  <th align="left">描述</th>
  <th align="left">文件</th>
</tr>
</thead>
<tbody><tr>
  <td align="left">ipc</td>
  <td align="left">进程间通信总控制调用</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left"><strong>信号</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sigaction</td>
  <td align="left">设置对指定信号的处理方法</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sigprocmask</td>
  <td align="left">根据参数对信号集中的信号执行阻塞/解除阻塞等操作</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sigpending</td>
  <td align="left">为指定的被阻塞信号设置队列</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sigsuspend</td>
  <td align="left">挂起进程等待特定信号</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">signal</td>
  <td align="left">参见signal</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">kill</td>
  <td align="left">向进程或进程组发信号</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr>
<tr>
  <td align="left">*sigblock</td>
  <td align="left">向被阻塞信号掩码中添加信号,已被sigprocmask代替</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">*siggetmask</td>
  <td align="left">取得现有阻塞信号掩码,已被sigprocmask代替</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left"></td>
  <td align="left">*sigsetmask</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">*sigmask</td>
  <td align="left">将给定的信号转化为掩码,已被sigprocmask代替</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">*sigpause</td>
  <td align="left">作用同sigsuspend,已被sigsuspend代替</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">sigvec</td>
  <td align="left">为兼容BSD而设的信号处理函数,作用类似sigaction</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">ssetmask</td>
  <td align="left">ANSI C的信号处理函数,作用类似sigaction</td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left"><strong>2、消息</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">msgctl</td>
  <td align="left">消息控制操作</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/msg.c" rel="nofollow">ipc/msg.c</a></td>
</tr>
<tr>
  <td align="left">msgget</td>
  <td align="left">获取消息队列</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/msg.c" rel="nofollow">ipc/msg.c</a></td>
</tr>
<tr>
  <td align="left">msgsnd</td>
  <td align="left">发消息</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/msg.c" rel="nofollow">ipc/msg.c</a></td>
</tr>
<tr>
  <td align="left">msgrcv</td>
  <td align="left">取消息</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/msg.c" rel="nofollow">ipc/msg.c</a></td>
</tr>
<tr>
  <td align="left"><strong>3、管道</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">pipe</td>
  <td align="left">创建管道</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/pipe.c" rel="nofollow">fs/pipe.c</a></td>
</tr>
<tr>
  <td align="left"><strong>4、信号量</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">semctl</td>
  <td align="left">信号量控制</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/sem.c" rel="nofollow">ipc/sem.c</a></td>
</tr>
<tr>
  <td align="left">semget</td>
  <td align="left">获取一组信号量</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/sem.c" rel="nofollow">ipc/sem.c</a></td>
</tr>
<tr>
  <td align="left">semop</td>
  <td align="left">信号量操作</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/sem.c" rel="nofollow">ipc/sem.c</a></td>
</tr>
<tr>
  <td align="left"><strong>5、共享内存</strong></td>
  <td align="left"></td>
  <td align="left"></td>
</tr>
<tr>
  <td align="left">shmctl</td>
  <td align="left">控制共享内存</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/shm.c" rel="nofollow">ipc/shm.c</a></td>
</tr>
<tr>
  <td align="left">shmget</td>
  <td align="left">获取共享内存</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/shm.c" rel="nofollow">ipc/shm.c</a></td>
</tr>
<tr>
  <td align="left">shmat</td>
  <td align="left">连接共享内存</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/shm.c" rel="nofollow">ipc/shm.c</a></td>
</tr>
<tr>
  <td align="left">shmdt</td>
  <td align="left">拆卸共享内存</td>
  <td align="left"><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/shm.c" rel="nofollow">ipc/shm.c</a></td>
</tr>
</tbody></table></div>


<hr>


<h2 style="font-weight: normal;">Linux系统调用表2 （附linux源码）</h2>

<table><thead><tr>
<td>系统调用号</td>
<td>函数名</td>
<td>入口点</td>
<td>源代码</td>
</tr></thead><tbody><tr><td>0</td>
    <td>read</td>
    <td>sys_read</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow">fs/read_write.c</a></td>
</tr><tr><td>1</td>
    <td>write</td>
    <td>sys_write</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow">fs/read_write.c</a></td>
</tr><tr><td>2</td>
    <td>open</td>
    <td>sys_open</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>3</td>
    <td>close</td>
    <td>sys_close</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>4</td>
    <td>stat</td>
    <td>sys_newstat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/stat.c" rel="nofollow">fs/stat.c</a></td>
</tr><tr><td>5</td>
    <td>fstat</td>
    <td>sys_newfstat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/stat.c" rel="nofollow">fs/stat.c</a></td>
</tr><tr><td>6</td>
    <td>lstat</td>
    <td>sys_newlstat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/stat.c" rel="nofollow">fs/stat.c</a></td>
</tr><tr><td>7</td>
    <td>poll</td>
    <td>sys_poll</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/select.c" rel="nofollow">fs/select.c</a></td>
</tr><tr><td>8</td>
    <td>lseek</td>
    <td>sys_lseek</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow">fs/read_write.c</a></td>
</tr><tr><td>9</td>
    <td>mmap</td>
    <td>sys_mmap</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/kernel/sys_x86_64.c" rel="nofollow">arch/x86/kernel/sys_x86_64.c</a></td>
</tr><tr><td>10</td>
    <td>mprotect</td>
    <td>sys_mprotect</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mprotect.c" rel="nofollow">mm/mprotect.c</a></td>
</tr><tr><td>11</td>
    <td>munmap</td>
    <td>sys_munmap</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mmap.c" rel="nofollow">mm/mmap.c</a></td>
</tr><tr><td>12</td>
    <td>brk</td>
    <td>sys_brk</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mmap.c" rel="nofollow">mm/mmap.c</a></td>
</tr><tr><td>13</td>
    <td>rt_sigaction</td>
    <td>sys_rt_sigaction</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>14</td>
    <td>rt_sigprocmask</td>
    <td>sys_rt_sigprocmask</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>15</td>
    <td>rt_sigreturn</td>
    <td>stub_rt_sigreturn</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/kernel/signal.c" rel="nofollow">arch/x86/kernel/signal.c</a></td>
</tr><tr><td>16</td>
    <td>ioctl</td>
    <td>sys_ioctl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/ioctl.c" rel="nofollow">fs/ioctl.c</a></td>
</tr><tr><td>17</td>
    <td>pread64</td>
    <td>sys_pread64</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow">fs/read_write.c</a></td>
</tr><tr><td>18</td>
    <td>pwrite64</td>
    <td>sys_pwrite64</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow">fs/read_write.c</a></td>
</tr><tr><td>19</td>
    <td>readv</td>
    <td>sys_readv</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow">fs/read_write.c</a></td>
</tr><tr><td>20</td>
    <td>writev</td>
    <td>sys_writev</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow">fs/read_write.c</a></td>
</tr><tr><td>21</td>
    <td>access</td>
    <td>sys_access</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>22</td>
    <td>pipe</td>
    <td>sys_pipe</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/pipe.c" rel="nofollow">fs/pipe.c</a></td>
</tr><tr><td>23</td>
    <td>select</td>
    <td>sys_select</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/select.c" rel="nofollow">fs/select.c</a></td>
</tr><tr><td>24</td>
    <td>sched_yield</td>
    <td>sys_sched_yield</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow">kernel/sched/core.c</a></td>
</tr><tr><td>25</td>
    <td>mremap</td>
    <td>sys_mremap</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mmap.c" rel="nofollow">mm/mmap.c</a></td>
</tr><tr><td>26</td>
    <td>msync</td>
    <td>sys_msync</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/msync.c" rel="nofollow">mm/msync.c</a></td>
</tr><tr><td>27</td>
    <td>mincore</td>
    <td>sys_mincore</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mincore.c" rel="nofollow">mm/mincore.c</a></td>
</tr><tr><td>28</td>
    <td>madvise</td>
    <td>sys_madvise</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/madvise.c" rel="nofollow">mm/madvise.c</a></td>
</tr><tr><td>29</td>
    <td>shmget</td>
    <td>sys_shmget</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/shm.c" rel="nofollow">ipc/shm.c</a></td>
</tr><tr><td>30</td>
    <td>shmat</td>
    <td>sys_shmat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/shm.c" rel="nofollow">ipc/shm.c</a></td>
</tr><tr><td>31</td>
    <td>shmctl</td>
    <td>sys_shmctl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/shm.c" rel="nofollow">ipc/shm.c</a></td>
</tr><tr><td>32</td>
    <td>dup</td>
    <td>sys_dup</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/file.c" rel="nofollow">fs/file.c</a></td>
</tr><tr><td>33</td>
    <td>dup2</td>
    <td>sys_dup2</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/file.c" rel="nofollow">fs/file.c</a></td>
</tr><tr><td>34</td>
    <td>pause</td>
    <td>sys_pause</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>35</td>
    <td>nanosleep</td>
    <td>sys_nanosleep</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/hrtimer.c" rel="nofollow">kernel/hrtimer.c</a></td>
</tr><tr><td>36</td>
    <td>getitimer</td>
    <td>sys_getitimer</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/itimer.c" rel="nofollow">kernel/itimer.c</a></td>
</tr><tr><td>37</td>
    <td>alarm</td>
    <td>sys_alarm</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/timer.c" rel="nofollow">kernel/timer.c</a></td>
</tr><tr><td>38</td>
    <td>setitimer</td>
    <td>sys_setitimer</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/itimer.c" rel="nofollow">kernel/itimer.c</a></td>
</tr><tr><td>39</td>
    <td>getpid</td>
    <td>sys_getpid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>40</td>
    <td>sendfile</td>
    <td>sys_sendfile64</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow">fs/read_write.c</a></td>
</tr><tr><td>41</td>
    <td>socket</td>
    <td>sys_socket</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>42</td>
    <td>connect</td>
    <td>sys_connect</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>43</td>
    <td>accept</td>
    <td>sys_accept</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>44</td>
    <td>sendto</td>
    <td>sys_sendto</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>45</td>
    <td>recvfrom</td>
    <td>sys_recvfrom</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>46</td>
    <td>sendmsg</td>
    <td>sys_sendmsg</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>47</td>
    <td>recvmsg</td>
    <td>sys_recvmsg</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>48</td>
    <td>shutdown</td>
    <td>sys_shutdown</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>49</td>
    <td>bind</td>
    <td>sys_bind</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>50</td>
    <td>listen</td>
    <td>sys_listen</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>51</td>
    <td>getsockname</td>
    <td>sys_getsockname</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>52</td>
    <td>getpeername</td>
    <td>sys_getpeername</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>53</td>
    <td>socketpair</td>
    <td>sys_socketpair</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>54</td>
    <td>setsockopt</td>
    <td>sys_setsockopt</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>55</td>
    <td>getsockopt</td>
    <td>sys_getsockopt</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>56</td>
    <td>clone</td>
    <td>stub_clone</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/fork.c" rel="nofollow">kernel/fork.c</a></td>
</tr><tr><td>57</td>
    <td>fork</td>
    <td>stub_fork</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/fork.c" rel="nofollow">kernel/fork.c</a></td>
</tr><tr><td>58</td>
    <td>vfork</td>
    <td>stub_vfork</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/fork.c" rel="nofollow">kernel/fork.c</a></td>
</tr><tr><td>59</td>
    <td>execve</td>
    <td>stub_execve</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/exec.c" rel="nofollow">fs/exec.c</a></td>
</tr><tr><td>60</td>
    <td>exit</td>
    <td>sys_exit</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/exit.c" rel="nofollow">kernel/exit.c</a></td>
</tr><tr><td>61</td>
    <td>wait4</td>
    <td>sys_wait4</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/exit.c" rel="nofollow">kernel/exit.c</a></td>
</tr><tr><td>62</td>
    <td>kill</td>
    <td>sys_kill</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>63</td>
    <td>uname</td>
    <td>sys_newuname</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>64</td>
    <td>semget</td>
    <td>sys_semget</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/sem.c" rel="nofollow">ipc/sem.c</a></td>
</tr><tr><td>65</td>
    <td>semop</td>
    <td>sys_semop</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/sem.c" rel="nofollow">ipc/sem.c</a></td>
</tr><tr><td>66</td>
    <td>semctl</td>
    <td>sys_semctl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/sem.c" rel="nofollow">ipc/sem.c</a></td>
</tr><tr><td>67</td>
    <td>shmdt</td>
    <td>sys_shmdt</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/shm.c" rel="nofollow">ipc/shm.c</a></td>
</tr><tr><td>68</td>
    <td>msgget</td>
    <td>sys_msgget</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/msg.c" rel="nofollow">ipc/msg.c</a></td>
</tr><tr><td>69</td>
    <td>msgsnd</td>
    <td>sys_msgsnd</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/msg.c" rel="nofollow">ipc/msg.c</a></td>
</tr><tr><td>70</td>
    <td>msgrcv</td>
    <td>sys_msgrcv</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/msg.c" rel="nofollow">ipc/msg.c</a></td>
</tr><tr><td>71</td>
    <td>msgctl</td>
    <td>sys_msgctl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/msg.c" rel="nofollow">ipc/msg.c</a></td>
</tr><tr><td>72</td>
    <td>fcntl</td>
    <td>sys_fcntl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/fcntl.c" rel="nofollow">fs/fcntl.c</a></td>
</tr><tr><td>73</td>
    <td>flock</td>
    <td>sys_flock</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/locks.c" rel="nofollow">fs/locks.c</a></td>
</tr><tr><td>74</td>
    <td>fsync</td>
    <td>sys_fsync</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/sync.c" rel="nofollow">fs/sync.c</a></td>
</tr><tr><td>75</td>
    <td>fdatasync</td>
    <td>sys_fdatasync</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/sync.c" rel="nofollow">fs/sync.c</a></td>
</tr><tr><td>76</td>
    <td>truncate</td>
    <td>sys_truncate</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>77</td>
    <td>ftruncate</td>
    <td>sys_ftruncate</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>78</td>
    <td>getdents</td>
    <td>sys_getdents</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/readdir.c" rel="nofollow">fs/readdir.c</a></td>
</tr><tr><td>79</td>
    <td>getcwd</td>
    <td>sys_getcwd</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/dcache.c" rel="nofollow">fs/dcache.c</a></td>
</tr><tr><td>80</td>
    <td>chdir</td>
    <td>sys_chdir</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>81</td>
    <td>fchdir</td>
    <td>sys_fchdir</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>82</td>
    <td>rename</td>
    <td>sys_rename</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>83</td>
    <td>mkdir</td>
    <td>sys_mkdir</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>84</td>
    <td>rmdir</td>
    <td>sys_rmdir</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>85</td>
    <td>creat</td>
    <td>sys_creat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>86</td>
    <td>link</td>
    <td>sys_link</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>87</td>
    <td>unlink</td>
    <td>sys_unlink</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>88</td>
    <td>symlink</td>
    <td>sys_symlink</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>89</td>
    <td>readlink</td>
    <td>sys_readlink</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/stat.c" rel="nofollow">fs/stat.c</a></td>
</tr><tr><td>90</td>
    <td>chmod</td>
    <td>sys_chmod</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>91</td>
    <td>fchmod</td>
    <td>sys_fchmod</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>92</td>
    <td>chown</td>
    <td>sys_chown</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>93</td>
    <td>fchown</td>
    <td>sys_fchown</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>94</td>
    <td>lchown</td>
    <td>sys_lchown</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>95</td>
    <td>umask</td>
    <td>sys_umask</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>96</td>
    <td>gettimeofday</td>
    <td>sys_gettimeofday</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/time.c" rel="nofollow">kernel/time.c</a></td>
</tr><tr><td>97</td>
    <td>getrlimit</td>
    <td>sys_getrlimit</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>98</td>
    <td>getrusage</td>
    <td>sys_getrusage</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>99</td>
    <td>sysinfo</td>
    <td>sys_sysinfo</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>100</td>
    <td>times</td>
    <td>sys_times</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>101</td>
    <td>ptrace</td>
    <td>sys_ptrace</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/ptrace.c" rel="nofollow">kernel/ptrace.c</a></td>
</tr><tr><td>102</td>
    <td>getuid</td>
    <td>sys_getuid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>103</td>
    <td>syslog</td>
    <td>sys_syslog</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/printk/printk.c" rel="nofollow">kernel/printk/printk.c</a></td>
</tr><tr><td>104</td>
    <td>getgid</td>
    <td>sys_getgid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>105</td>
    <td>setuid</td>
    <td>sys_setuid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>106</td>
    <td>setgid</td>
    <td>sys_setgid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>107</td>
    <td>geteuid</td>
    <td>sys_geteuid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>108</td>
    <td>getegid</td>
    <td>sys_getegid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>109</td>
    <td>setpgid</td>
    <td>sys_setpgid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>110</td>
    <td>getppid</td>
    <td>sys_getppid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>111</td>
    <td>getpgrp</td>
    <td>sys_getpgrp</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>112</td>
    <td>setsid</td>
    <td>sys_setsid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>113</td>
    <td>setreuid</td>
    <td>sys_setreuid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>114</td>
    <td>setregid</td>
    <td>sys_setregid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>115</td>
    <td>getgroups</td>
    <td>sys_getgroups</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/groups.c" rel="nofollow">kernel/groups.c</a></td>
</tr><tr><td>116</td>
    <td>setgroups</td>
    <td>sys_setgroups</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/groups.c" rel="nofollow">kernel/groups.c</a></td>
</tr><tr><td>117</td>
    <td>setresuid</td>
    <td>sys_setresuid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>118</td>
    <td>getresuid</td>
    <td>sys_getresuid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>119</td>
    <td>setresgid</td>
    <td>sys_setresgid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>120</td>
    <td>getresgid</td>
    <td>sys_getresgid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>121</td>
    <td>getpgid</td>
    <td>sys_getpgid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>122</td>
    <td>setfsuid</td>
    <td>sys_setfsuid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>123</td>
    <td>setfsgid</td>
    <td>sys_setfsgid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>124</td>
    <td>getsid</td>
    <td>sys_getsid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>125</td>
    <td>capget</td>
    <td>sys_capget</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/capability.c" rel="nofollow">kernel/capability.c</a></td>
</tr><tr><td>126</td>
    <td>capset</td>
    <td>sys_capset</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/capability.c" rel="nofollow">kernel/capability.c</a></td>
</tr><tr><td>127</td>
    <td>rt_sigpending</td>
    <td>sys_rt_sigpending</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>128</td>
    <td>rt_sigtimedwait</td>
    <td>sys_rt_sigtimedwait</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>129</td>
    <td>rt_sigqueueinfo</td>
    <td>sys_rt_sigqueueinfo</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>130</td>
    <td>rt_sigsuspend</td>
    <td>sys_rt_sigsuspend</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>131</td>
    <td>sigaltstack</td>
    <td>sys_sigaltstack</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>132</td>
    <td>utime</td>
    <td>sys_utime</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/utimes.c" rel="nofollow">fs/utimes.c</a></td>
</tr><tr><td>133</td>
    <td>mknod</td>
    <td>sys_mknod</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>134</td>
    <td>uselib</td>
    <td>&nbsp;</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/exec.c" rel="nofollow">fs/exec.c</a></td>
</tr><tr><td>135</td>
    <td>personality</td>
    <td>sys_personality</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/exec_domain.c" rel="nofollow">kernel/exec_domain.c</a></td>
</tr><tr><td>136</td>
    <td>ustat</td>
    <td>sys_ustat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/statfs.c" rel="nofollow">fs/statfs.c</a></td>
</tr><tr><td>137</td>
    <td>statfs</td>
    <td>sys_statfs</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/statfs.c" rel="nofollow">fs/statfs.c</a></td>
</tr><tr><td>138</td>
    <td>fstatfs</td>
    <td>sys_fstatfs</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/statfs.c" rel="nofollow">fs/statfs.c</a></td>
</tr><tr><td>139</td>
    <td>sysfs</td>
    <td>sys_sysfs</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/filesystems.c" rel="nofollow">fs/filesystems.c</a></td>
</tr><tr><td>140</td>
    <td>getpriority</td>
    <td>sys_getpriority</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>141</td>
    <td>setpriority</td>
    <td>sys_setpriority</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>142</td>
    <td>sched_setparam</td>
    <td>sys_sched_setparam</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow">kernel/sched/core.c</a></td>
</tr><tr><td>143</td>
    <td>sched_getparam</td>
    <td>sys_sched_getparam</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow">kernel/sched/core.c</a></td>
</tr><tr><td>144</td>
    <td>sched_setscheduler</td>
    <td>sys_sched_setscheduler</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow">kernel/sched/core.c</a></td>
</tr><tr><td>145</td>
    <td>sched_getscheduler</td>
    <td>sys_sched_getscheduler</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow">kernel/sched/core.c</a></td>
</tr><tr><td>146</td>
    <td>sched_get_priority_max</td>
    <td>sys_sched_get_priority_max</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow">kernel/sched/core.c</a></td>
</tr><tr><td>147</td>
    <td>sched_get_priority_min</td>
    <td>sys_sched_get_priority_min</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow">kernel/sched/core.c</a></td>
</tr><tr><td>148</td>
    <td>sched_rr_get_interval</td>
    <td>sys_sched_rr_get_interval</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow">kernel/sched/core.c</a></td>
</tr><tr><td>149</td>
    <td>mlock</td>
    <td>sys_mlock</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mlock.c" rel="nofollow">mm/mlock.c</a></td>
</tr><tr><td>150</td>
    <td>munlock</td>
    <td>sys_munlock</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mlock.c" rel="nofollow">mm/mlock.c</a></td>
</tr><tr><td>151</td>
    <td>mlockall</td>
    <td>sys_mlockall</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mlock.c" rel="nofollow">mm/mlock.c</a></td>
</tr><tr><td>152</td>
    <td>munlockall</td>
    <td>sys_munlockall</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mlock.c" rel="nofollow">mm/mlock.c</a></td>
</tr><tr><td>153</td>
    <td>vhangup</td>
    <td>sys_vhangup</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>154</td>
    <td>modify_ldt</td>
    <td>sys_modify_ldt</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/um/ldt.c" rel="nofollow">arch/x86/um/ldt.c</a></td>
</tr><tr><td>155</td>
    <td>pivot_root</td>
    <td>sys_pivot_root</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namespace.c" rel="nofollow">fs/namespace.c</a></td>
</tr><tr><td>156</td>
    <td>_sysctl</td>
    <td>sys_sysctl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sysctl_binary.c" rel="nofollow">kernel/sysctl_binary.c</a></td>
</tr><tr><td>157</td>
    <td>prctl</td>
    <td>sys_prctl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>158</td>
    <td>arch_prctl</td>
    <td>sys_arch_prctl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/um/syscalls_64.c" rel="nofollow">arch/x86/um/syscalls_64.c</a></td>
</tr><tr><td>159</td>
    <td>adjtimex</td>
    <td>sys_adjtimex</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/time.c" rel="nofollow">kernel/time.c</a></td>
</tr><tr><td>160</td>
    <td>setrlimit</td>
    <td>sys_setrlimit</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>161</td>
    <td>chroot</td>
    <td>sys_chroot</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>162</td>
    <td>sync</td>
    <td>sys_sync</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/sync.c" rel="nofollow">fs/sync.c</a></td>
</tr><tr><td>163</td>
    <td>acct</td>
    <td>sys_acct</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/acct.c" rel="nofollow">kernel/acct.c</a></td>
</tr><tr><td>164</td>
    <td>settimeofday</td>
    <td>sys_settimeofday</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/time.c" rel="nofollow">kernel/time.c</a></td>
</tr><tr><td>165</td>
    <td>mount</td>
    <td>sys_mount</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namespace.c" rel="nofollow">fs/namespace.c</a></td>
</tr><tr><td>166</td>
    <td>umount2</td>
    <td>sys_umount</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namespace.c" rel="nofollow">fs/namespace.c</a></td>
</tr><tr><td>167</td>
    <td>swapon</td>
    <td>sys_swapon</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/swapfile.c" rel="nofollow">mm/swapfile.c</a></td>
</tr><tr><td>168</td>
    <td>swapoff</td>
    <td>sys_swapoff</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/swapfile.c" rel="nofollow">mm/swapfile.c</a></td>
</tr><tr><td>169</td>
    <td>reboot</td>
    <td>sys_reboot</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/reboot.c" rel="nofollow">kernel/reboot.c</a></td>
</tr><tr><td>170</td>
    <td>sethostname</td>
    <td>sys_sethostname</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>171</td>
    <td>setdomainname</td>
    <td>sys_setdomainname</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>172</td>
    <td>iopl</td>
    <td>stub_iopl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/kernel/ioport.c" rel="nofollow">arch/x86/kernel/ioport.c</a></td>
</tr><tr><td>173</td>
    <td>ioperm</td>
    <td>sys_ioperm</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/kernel/ioport.c" rel="nofollow">arch/x86/kernel/ioport.c</a></td>
</tr><tr><td>174</td>
    <td>create_module</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>175</td>
    <td>init_module</td>
    <td>sys_init_module</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/module.c" rel="nofollow">kernel/module.c</a></td>
</tr><tr><td>176</td>
    <td>delete_module</td>
    <td>sys_delete_module</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/module.c" rel="nofollow">kernel/module.c</a></td>
</tr><tr><td>177</td>
    <td>get_kernel_syms</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>178</td>
    <td>query_module</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>179</td>
    <td>quotactl</td>
    <td>sys_quotactl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/quota/quota.c" rel="nofollow">fs/quota/quota.c</a></td>
</tr><tr><td>180</td>
    <td>nfsservctl</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>181</td>
    <td>getpmsg</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>182</td>
    <td>putpmsg</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>183</td>
    <td>afs_syscall</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>184</td>
    <td>tuxcall</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>185</td>
    <td>security</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>186</td>
    <td>gettid</td>
    <td>sys_gettid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>187</td>
    <td>readahead</td>
    <td>sys_readahead</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/readahead.c" rel="nofollow">mm/readahead.c</a></td>
</tr><tr><td>188</td>
    <td>setxattr</td>
    <td>sys_setxattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>189</td>
    <td>lsetxattr</td>
    <td>sys_lsetxattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>190</td>
    <td>fsetxattr</td>
    <td>sys_fsetxattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>191</td>
    <td>getxattr</td>
    <td>sys_getxattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>192</td>
    <td>lgetxattr</td>
    <td>sys_lgetxattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>193</td>
    <td>fgetxattr</td>
    <td>sys_fgetxattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>194</td>
    <td>listxattr</td>
    <td>sys_listxattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>195</td>
    <td>llistxattr</td>
    <td>sys_llistxattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>196</td>
    <td>flistxattr</td>
    <td>sys_flistxattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>197</td>
    <td>removexattr</td>
    <td>sys_removexattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>198</td>
    <td>lremovexattr</td>
    <td>sys_lremovexattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>199</td>
    <td>fremovexattr</td>
    <td>sys_fremovexattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/xattr.c" rel="nofollow">fs/xattr.c</a></td>
</tr><tr><td>200</td>
    <td>tkill</td>
    <td>sys_tkill</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>201</td>
    <td>time</td>
    <td>sys_time</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/time.c" rel="nofollow">kernel/time.c</a></td>
</tr><tr><td>202</td>
    <td>futex</td>
    <td>sys_futex</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/futex.c" rel="nofollow">kernel/futex.c</a></td>
</tr><tr><td>203</td>
    <td>sched_setaffinity</td>
    <td>sys_sched_setaffinity</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow">kernel/sched/core.c</a></td>
</tr><tr><td>204</td>
    <td>sched_getaffinity</td>
    <td>sys_sched_getaffinity</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sched/core.c" rel="nofollow">kernel/sched/core.c</a></td>
</tr><tr><td>205</td>
    <td>set_thread_area</td>
    <td>&nbsp;</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/kernel/tls.c" rel="nofollow">arch/x86/kernel/tls.c</a></td>
</tr><tr><td>206</td>
    <td>io_setup</td>
    <td>sys_io_setup</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/aio.c" rel="nofollow">fs/aio.c</a></td>
</tr><tr><td>207</td>
    <td>io_destroy</td>
    <td>sys_io_destroy</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/aio.c" rel="nofollow">fs/aio.c</a></td>
</tr><tr><td>208</td>
    <td>io_getevents</td>
    <td>sys_io_getevents</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/aio.c" rel="nofollow">fs/aio.c</a></td>
</tr><tr><td>209</td>
    <td>io_submit</td>
    <td>sys_io_submit</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/aio.c" rel="nofollow">fs/aio.c</a></td>
</tr><tr><td>210</td>
    <td>io_cancel</td>
    <td>sys_io_cancel</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/aio.c" rel="nofollow">fs/aio.c</a></td>
</tr><tr><td>211</td>
    <td>get_thread_area</td>
    <td>&nbsp;</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/arch/x86/kernel/tls.c" rel="nofollow">arch/x86/kernel/tls.c</a></td>
</tr><tr><td>212</td>
    <td>lookup_dcookie</td>
    <td>sys_lookup_dcookie</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/dcookies.c" rel="nofollow">fs/dcookies.c</a></td>
</tr><tr><td>213</td>
    <td>epoll_create</td>
    <td>sys_epoll_create</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/eventpoll.c" rel="nofollow">fs/eventpoll.c</a></td>
</tr><tr><td>214</td>
    <td>epoll_ctl_old</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>215</td>
    <td>epoll_wait_old</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>216</td>
    <td>remap_file_pages</td>
    <td>sys_remap_file_pages</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/fremap.c" rel="nofollow">mm/fremap.c</a></td>
</tr><tr><td>217</td>
    <td>getdents64</td>
    <td>sys_getdents64</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/readdir.c" rel="nofollow">fs/readdir.c</a></td>
</tr><tr><td>218</td>
    <td>set_tid_address</td>
    <td>sys_set_tid_address</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/fork.c" rel="nofollow">kernel/fork.c</a></td>
</tr><tr><td>219</td>
    <td>restart_syscall</td>
    <td>sys_restart_syscall</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>220</td>
    <td>semtimedop</td>
    <td>sys_semtimedop</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/sem.c" rel="nofollow">ipc/sem.c</a></td>
</tr><tr><td>221</td>
    <td>fadvise64</td>
    <td>sys_fadvise64</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/fadvise.c" rel="nofollow">mm/fadvise.c</a></td>
</tr><tr><td>222</td>
    <td>timer_create</td>
    <td>sys_timer_create</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/posix-timers.c" rel="nofollow">kernel/posix-timers.c</a></td>
</tr><tr><td>223</td>
    <td>timer_settime</td>
    <td>sys_timer_settime</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/posix-timers.c" rel="nofollow">kernel/posix-timers.c</a></td>
</tr><tr><td>224</td>
    <td>timer_gettime</td>
    <td>sys_timer_gettime</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/posix-timers.c" rel="nofollow">kernel/posix-timers.c</a></td>
</tr><tr><td>225</td>
    <td>timer_getoverrun</td>
    <td>sys_timer_getoverrun</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/posix-timers.c" rel="nofollow">kernel/posix-timers.c</a></td>
</tr><tr><td>226</td>
    <td>timer_delete</td>
    <td>sys_timer_delete</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/posix-timers.c" rel="nofollow">kernel/posix-timers.c</a></td>
</tr><tr><td>227</td>
    <td>clock_settime</td>
    <td>sys_clock_settime</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/posix-timers.c" rel="nofollow">kernel/posix-timers.c</a></td>
</tr><tr><td>228</td>
    <td>clock_gettime</td>
    <td>sys_clock_gettime</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/posix-timers.c" rel="nofollow">kernel/posix-timers.c</a></td>
</tr><tr><td>229</td>
    <td>clock_getres</td>
    <td>sys_clock_getres</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/posix-timers.c" rel="nofollow">kernel/posix-timers.c</a></td>
</tr><tr><td>230</td>
    <td>clock_nanosleep</td>
    <td>sys_clock_nanosleep</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/posix-timers.c" rel="nofollow">kernel/posix-timers.c</a></td>
</tr><tr><td>231</td>
    <td>exit_group</td>
    <td>sys_exit_group</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/exit.c" rel="nofollow">kernel/exit.c</a></td>
</tr><tr><td>232</td>
    <td>epoll_wait</td>
    <td>sys_epoll_wait</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/eventpoll.c" rel="nofollow">fs/eventpoll.c</a></td>
</tr><tr><td>233</td>
    <td>epoll_ctl</td>
    <td>sys_epoll_ctl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/eventpoll.c" rel="nofollow">fs/eventpoll.c</a></td>
</tr><tr><td>234</td>
    <td>tgkill</td>
    <td>sys_tgkill</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>235</td>
    <td>utimes</td>
    <td>sys_utimes</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/utimes.c" rel="nofollow">fs/utimes.c</a></td>
</tr><tr><td>236</td>
    <td>vserver</td>
    <td>&nbsp;</td>
    <td>NOT IMPLEMENTED</td>
</tr><tr><td>237</td>
    <td>mbind</td>
    <td>sys_mbind</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mempolicy.c" rel="nofollow">mm/mempolicy.c</a></td>
</tr><tr><td>238</td>
    <td>set_mempolicy</td>
    <td>sys_set_mempolicy</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mempolicy.c" rel="nofollow">mm/mempolicy.c</a></td>
</tr><tr><td>239</td>
    <td>get_mempolicy</td>
    <td>sys_get_mempolicy</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mempolicy.c" rel="nofollow">mm/mempolicy.c</a></td>
</tr><tr><td>240</td>
    <td>mq_open</td>
    <td>sys_mq_open</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/mqueue.c" rel="nofollow">ipc/mqueue.c</a></td>
</tr><tr><td>241</td>
    <td>mq_unlink</td>
    <td>sys_mq_unlink</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/mqueue.c" rel="nofollow">ipc/mqueue.c</a></td>
</tr><tr><td>242</td>
    <td>mq_timedsend</td>
    <td>sys_mq_timedsend</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/mqueue.c" rel="nofollow">ipc/mqueue.c</a></td>
</tr><tr><td>243</td>
    <td>mq_timedreceive</td>
    <td>sys_mq_timedreceive</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/mqueue.c" rel="nofollow">ipc/mqueue.c</a></td>
</tr><tr><td>244</td>
    <td>mq_notify</td>
    <td>sys_mq_notify</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/mqueue.c" rel="nofollow">ipc/mqueue.c</a></td>
</tr><tr><td>245</td>
    <td>mq_getsetattr</td>
    <td>sys_mq_getsetattr</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/ipc/mqueue.c" rel="nofollow">ipc/mqueue.c</a></td>
</tr><tr><td>246</td>
    <td>kexec_load</td>
    <td>sys_kexec_load</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/kexec.c" rel="nofollow">kernel/kexec.c</a></td>
</tr><tr><td>247</td>
    <td>waitid</td>
    <td>sys_waitid</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/exit.c" rel="nofollow">kernel/exit.c</a></td>
</tr><tr><td>248</td>
    <td>add_key</td>
    <td>sys_add_key</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/security/keys/keyctl.c" rel="nofollow">security/keys/keyctl.c</a></td>
</tr><tr><td>249</td>
    <td>request_key</td>
    <td>sys_request_key</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/security/keys/keyctl.c" rel="nofollow">security/keys/keyctl.c</a></td>
</tr><tr><td>250</td>
    <td>keyctl</td>
    <td>sys_keyctl</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/security/keys/keyctl.c" rel="nofollow">security/keys/keyctl.c</a></td>
</tr><tr><td>251</td>
    <td>ioprio_set</td>
    <td>sys_ioprio_set</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/ioprio.c" rel="nofollow">fs/ioprio.c</a></td>
</tr><tr><td>252</td>
    <td>ioprio_get</td>
    <td>sys_ioprio_get</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/ioprio.c" rel="nofollow">fs/ioprio.c</a></td>
</tr><tr><td>253</td>
    <td>inotify_init</td>
    <td>sys_inotify_init</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/notify/inotify/inotify_user.c" rel="nofollow">fs/notify/inotify/inotify_user.c</a></td>
</tr><tr><td>254</td>
    <td>inotify_add_watch</td>
    <td>sys_inotify_add_watch</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/notify/inotify/inotify_user.c" rel="nofollow">fs/notify/inotify/inotify_user.c</a></td>
</tr><tr><td>255</td>
    <td>inotify_rm_watch</td>
    <td>sys_inotify_rm_watch</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/notify/inotify/inotify_user.c" rel="nofollow">fs/notify/inotify/inotify_user.c</a></td>
</tr><tr><td>256</td>
    <td>migrate_pages</td>
    <td>sys_migrate_pages</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/mempolicy.c" rel="nofollow">mm/mempolicy.c</a></td>
</tr><tr><td>257</td>
    <td>openat</td>
    <td>sys_openat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>258</td>
    <td>mkdirat</td>
    <td>sys_mkdirat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>259</td>
    <td>mknodat</td>
    <td>sys_mknodat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>260</td>
    <td>fchownat</td>
    <td>sys_fchownat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>261</td>
    <td>futimesat</td>
    <td>sys_futimesat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/utimes.c" rel="nofollow">fs/utimes.c</a></td>
</tr><tr><td>262</td>
    <td>newfstatat</td>
    <td>sys_newfstatat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/stat.c" rel="nofollow">fs/stat.c</a></td>
</tr><tr><td>263</td>
    <td>unlinkat</td>
    <td>sys_unlinkat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>264</td>
    <td>renameat</td>
    <td>sys_renameat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>265</td>
    <td>linkat</td>
    <td>sys_linkat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>266</td>
    <td>symlinkat</td>
    <td>sys_symlinkat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/namei.c" rel="nofollow">fs/namei.c</a></td>
</tr><tr><td>267</td>
    <td>readlinkat</td>
    <td>sys_readlinkat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/stat.c" rel="nofollow">fs/stat.c</a></td>
</tr><tr><td>268</td>
    <td>fchmodat</td>
    <td>sys_fchmodat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>269</td>
    <td>faccessat</td>
    <td>sys_faccessat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>270</td>
    <td>pselect6</td>
    <td>sys_pselect6</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/select.c" rel="nofollow">fs/select.c</a></td>
</tr><tr><td>271</td>
    <td>ppoll</td>
    <td>sys_ppoll</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/select.c" rel="nofollow">fs/select.c</a></td>
</tr><tr><td>272</td>
    <td>unshare</td>
    <td>sys_unshare</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/fork.c" rel="nofollow">kernel/fork.c</a></td>
</tr><tr><td>273</td>
    <td>set_robust_list</td>
    <td>sys_set_robust_list</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/futex.c" rel="nofollow">kernel/futex.c</a></td>
</tr><tr><td>274</td>
    <td>get_robust_list</td>
    <td>sys_get_robust_list</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/futex.c" rel="nofollow">kernel/futex.c</a></td>
</tr><tr><td>275</td>
    <td>splice</td>
    <td>sys_splice</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/splice.c" rel="nofollow">fs/splice.c</a></td>
</tr><tr><td>276</td>
    <td>tee</td>
    <td>sys_tee</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/splice.c" rel="nofollow">fs/splice.c</a></td>
</tr><tr><td>277</td>
    <td>sync_file_range</td>
    <td>sys_sync_file_range</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/sync.c" rel="nofollow">fs/sync.c</a></td>
</tr><tr><td>278</td>
    <td>vmsplice</td>
    <td>sys_vmsplice</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/splice.c" rel="nofollow">fs/splice.c</a></td>
</tr><tr><td>279</td>
    <td>move_pages</td>
    <td>sys_move_pages</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/migrate.c" rel="nofollow">mm/migrate.c</a></td>
</tr><tr><td>280</td>
    <td>utimensat</td>
    <td>sys_utimensat</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/utimes.c" rel="nofollow">fs/utimes.c</a></td>
</tr><tr><td>281</td>
    <td>epoll_pwait</td>
    <td>sys_epoll_pwait</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/eventpoll.c" rel="nofollow">fs/eventpoll.c</a></td>
</tr><tr><td>282</td>
    <td>signalfd</td>
    <td>sys_signalfd</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/signalfd.c" rel="nofollow">fs/signalfd.c</a></td>
</tr><tr><td>283</td>
    <td>timerfd_create</td>
    <td>sys_timerfd_create</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/timerfd.c" rel="nofollow">fs/timerfd.c</a></td>
</tr><tr><td>284</td>
    <td>eventfd</td>
    <td>sys_eventfd</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/eventfd.c" rel="nofollow">fs/eventfd.c</a></td>
</tr><tr><td>285</td>
    <td>fallocate</td>
    <td>sys_fallocate</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/open.c" rel="nofollow">fs/open.c</a></td>
</tr><tr><td>286</td>
    <td>timerfd_settime</td>
    <td>sys_timerfd_settime</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/timerfd.c" rel="nofollow">fs/timerfd.c</a></td>
</tr><tr><td>287</td>
    <td>timerfd_gettime</td>
    <td>sys_timerfd_gettime</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/timerfd.c" rel="nofollow">fs/timerfd.c</a></td>
</tr><tr><td>288</td>
    <td>accept4</td>
    <td>sys_accept4</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>289</td>
    <td>signalfd4</td>
    <td>sys_signalfd4</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/signalfd.c" rel="nofollow">fs/signalfd.c</a></td>
</tr><tr><td>290</td>
    <td>eventfd2</td>
    <td>sys_eventfd2</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/eventfd.c" rel="nofollow">fs/eventfd.c</a></td>
</tr><tr><td>291</td>
    <td>epoll_create1</td>
    <td>sys_epoll_create1</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/eventpoll.c" rel="nofollow">fs/eventpoll.c</a></td>
</tr><tr><td>292</td>
    <td>dup3</td>
    <td>sys_dup3</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/file.c" rel="nofollow">fs/file.c</a></td>
</tr><tr><td>293</td>
    <td>pipe2</td>
    <td>sys_pipe2</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/pipe.c" rel="nofollow">fs/pipe.c</a></td>
</tr><tr><td>294</td>
    <td>inotify_init1</td>
    <td>sys_inotify_init1</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/notify/inotify/inotify_user.c" rel="nofollow">fs/notify/inotify/inotify_user.c</a></td>
</tr><tr><td>295</td>
    <td>preadv</td>
    <td>sys_preadv</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow">fs/read_write.c</a></td>
</tr><tr><td>296</td>
    <td>pwritev</td>
    <td>sys_pwritev</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/read_write.c" rel="nofollow">fs/read_write.c</a></td>
</tr><tr><td>297</td>
    <td>rt_tgsigqueueinfo</td>
    <td>sys_rt_tgsigqueueinfo</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/signal.c" rel="nofollow">kernel/signal.c</a></td>
</tr><tr><td>298</td>
    <td>perf_event_open</td>
    <td>sys_perf_event_open</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/events/core.c" rel="nofollow">kernel/events/core.c</a></td>
</tr><tr><td>299</td>
    <td>recvmmsg</td>
    <td>sys_recvmmsg</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>300</td>
    <td>fanotify_init</td>
    <td>sys_fanotify_init</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/notify/fanotify/fanotify_user.c" rel="nofollow">fs/notify/fanotify/fanotify_user.c</a></td>
</tr><tr><td>301</td>
    <td>fanotify_mark</td>
    <td>sys_fanotify_mark</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/notify/fanotify/fanotify_user.c" rel="nofollow">fs/notify/fanotify/fanotify_user.c</a></td>
</tr><tr><td>302</td>
    <td>prlimit64</td>
    <td>sys_prlimit64</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>303</td>
    <td>name_to_handle_at</td>
    <td>sys_name_to_handle_at</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/fhandle.c" rel="nofollow">fs/fhandle.c</a></td>
</tr><tr><td>304</td>
    <td>open_by_handle_at</td>
    <td>sys_open_by_handle_at</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/fhandle.c" rel="nofollow">fs/fhandle.c</a></td>
</tr><tr><td>305</td>
    <td>clock_adjtime</td>
    <td>sys_clock_adjtime</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/posix-timers.c" rel="nofollow">kernel/posix-timers.c</a></td>
</tr><tr><td>306</td>
    <td>syncfs</td>
    <td>sys_syncfs</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/fs/sync.c" rel="nofollow">fs/sync.c</a></td>
</tr><tr><td>307</td>
    <td>sendmmsg</td>
    <td>sys_sendmmsg</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/net/socket.c" rel="nofollow">net/socket.c</a></td>
</tr><tr><td>308</td>
    <td>setns</td>
    <td>sys_setns</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/nsproxy.c" rel="nofollow">kernel/nsproxy.c</a></td>
</tr><tr><td>309</td>
    <td>getcpu</td>
    <td>sys_getcpu</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/sys.c" rel="nofollow">kernel/sys.c</a></td>
</tr><tr><td>310</td>
    <td>process_vm_readv</td>
    <td>sys_process_vm_readv</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/process_vm_access.c" rel="nofollow">mm/process_vm_access.c</a></td>
</tr><tr><td>311</td>
    <td>process_vm_writev</td>
    <td>sys_process_vm_writev</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/mm/process_vm_access.c" rel="nofollow">mm/process_vm_access.c</a></td>
</tr><tr><td>312</td>
    <td>kcmp</td>
    <td>sys_kcmp</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/kcmp.c" rel="nofollow">kernel/kcmp.c</a></td>
</tr><tr><td>313</td>
    <td>finit_module</td>
    <td>sys_finit_module</td>
    <td><a href="https://git.kernel.org/cgit/linux/kernel/git/torvalds/linux.git/tree/kernel/module.c" rel="nofollow">kernel/module.c</a></td>
</tr></tbody></table>

<hr>
