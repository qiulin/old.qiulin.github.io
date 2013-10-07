---
layout: post
title: Glusterd服务init.d脚本分析2
tags: [GlusterFS, 填坑]
image:
  feature: abstract-10.jpg
  credit: dargadgetz
  creditlink: http://www.dargadgetz.com/ios-7-abstract-wallpaper-pack-for-iphone-5-and-ipod-touch-retina/
comments: true
share: true  
---

这篇算是真正的填坑贴，之前只是贴出了Glusterd的initd文件（[Glusterd服务init.d脚本分析](http://blog.qlin.net/2013/09/16/glusterd-initd-file/)），并没有作详细的分析，
十一假期马上就要结束了，需要把这个坑给填了。

下面就把该文件中的主要操作做一下解释。

>  . /etc/rc.d/init.d/functions

这一步是引入functions文件，functions可以算是linux里面的一个shell函数库，
/etc/init.d目录下很多文件都会用到这个函数库，主要提供一些脚本的基础功能。

functions首先会设置umask，path和语言环境，然后会设置success，failure，warning，normal几种情况下的字体颜色。

functions还提供了下面这些主要方法：

checkpid：检查是否已存在pid，如果已经存在，则返回0（通过查看/proc目录的方式）

daemon：启动某个服务。/etc/init.d目录部分脚本的start使用到了这个。

killproc：杀死某个进程。/etc/init.d目录中的部分脚本的stop操作会用到这个。

pidfileofproc：查找某个进程的pid。

pidofproc：类似上者，只是还查找了pidof命令。

status：返回一个服务的状态。

echo_success, echo_failure, echo_passed, echo_warning：分别输出各类信息

success, failure, passed, warning：分别记录日志并调用相应的方法。

action：打印某个信息并执行给定的命令，它会根据命令执行的结果来调用success, failure方法。

strstr：判断$1是否含有$2。

confirm：显示“Start service $1(Y)es/(N)o/(C)ontinue?[Y]”的提示信息，并返回选择结果。

> BASE=glusterd

设置基本的服务名，方便以后复用。

> [ -e /run ] && RUNDIR="/run"

> PIDFILE="${RUNDIR:-/var/run}/${BASE}.pid"

设置运行目录run和pid文件

> PID=`test -f $PIDFILE && cat $PIDFILE`

获取pid

> LOG_LEVEL=''

> LOG_FILE=''

> GLUSTERD_OPTIONS=''

> GLUSTERD_NOFILE='65536'

覆盖sysconfig文件夹中的相应设置。

> [ -f /etc/sysconfig/${BASE} ] && . /etc/sysconfig/${BASE}

如果在/etc/sysconfig/文件夹中存在相应的配置文件，则导入文件。

> [ ! -z $LOG_LEVEL ] && GLUSTERD_OPTIONS="${GLUSTERD_OPTIONS} --log-level ${LOG_LEVEL}"
> [ ! -z $LOG_FILE ] && GLUSTERD_OPTIONS="${GLUSTERD_OPTIONS} --log-file ${LOG_FILE}"

写一些配置

> GLUSTERFSD=glusterfsd
> GLUSTERFS=glusterfs
> GLUSTERD_BIN=/usr/sbin/$BASE
> GLUSTERD_OPTS="--pid-file=$PIDFILE ${GLUSTERD_OPTIONS}"
> GLUSTERD="$GLUSTERD_BIN $GLUSTERD_OPTS"
> RETVAL=0

配置变量和路径

> LOCKFILE=/var/lock/subsys/${BASE}

设置锁文件

下面介绍一个主要的操作

**start**

先检查是否已经有实例运行，如果没有则启动，如果有则作出提示。

**stop**

当然是start的相反过程，删除pidfile，并杀掉进程。

**restart**

重启，停掉，然后再起来。

**reload**

同restart

**force_reload**

同restart

**rh_status**

输出状态

剩下就是一些处理流程之类的，没必要一步步介绍了。一些细节的东西搞的还是不太明白，
待以后具体研究把。

-EOF-
