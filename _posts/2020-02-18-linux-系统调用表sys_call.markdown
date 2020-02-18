---
layout: post
title:  "linux-系统调用表sys_call"
tags: linux
---

### 概览 (IO, 内存， 进程)

![SystemCallInterface](../../../images/postimg/SCI_system_call_interface.png)


### Linux系统调用表

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


来自ibm.com

[https://www.ibm.com/developerworks/cn/linux/kernel/syscall/part1/appendix.html](https://www.ibm.com/developerworks/cn/linux/kernel/syscall/part1/appendix.html "https://www.ibm.com/developerworks/cn/linux/kernel/syscall/part1/appendix.html")

---
