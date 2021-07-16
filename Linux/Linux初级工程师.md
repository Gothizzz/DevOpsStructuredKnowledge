## 权限管理

### 1. Linux用户及权限

#### 1. Linux用户和组

##### Linux中的用户

Linux是一个多用户系统，Linux允许使用者在Linux系统上通过规划不同类型、不同层级的用户，并公平的分配系统资源与工作环境。不仅如此，和Windows不同的是，Linux允许不同的用户同时登录主机，同时使用主机的资源，因此Linux被称为多用户系统。

Linux以“用户与用户组”的概念，建立用户与文件权限之间的联系，保证系统能够充分考虑每个用户的隐私保护，很大程度上保障了Linux作为多用户系统的可行性。



##### root用户

root用户在Linux计算机中拥有全部权限。

在Linux中执行涉及到系统的命令一般都需要root权限，尤其是影响系统文件的命令。

由于root权限如此强大，所以建议只有必要时才使用，而不是直接以root用户身份进行登录，这样可以避免重要系统文件意外受损。

使用root用户创建新的用户，并授予必要的权限，在日常工作中使用对应的普通用户进行工作。



##### 系统用户

除了日常操作的用户以外，还会有一些其他用户，这些用户默认无法登陆系统。

这些用户的存在主要是为了满足系统进程对文件属主的需求。



##### 用户组

在linux中可以创建用户组来管理用户。

根据功能分类，可以分为：管理员组和普通用户组。

按类别分类，可以分为：基本组和附加组，一个用户只能有一个基本组，但可以有多个附加组。

按组本身的类别分类：公共组和私有组。私有组只有一个用户，且组名和用户名一致；公共组会有多个用户。



#### 2. Linux权限构成

##### Linux的权限组成

Linux下权限可以分为三类：User权限（u），Group权限（g），Other权限（o）

- User权限表示文件所有者；
- Group权限表示文件所有者所在的组
- Other表示所有其他用户

**![image-20210702003728097](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702003728097.png)**

##### Linux的权限分类

Linux将权限分为Read（读），Write（写），Execute（执行）三个不同的基本类别

- Read读权限表示：

针对**目录**，有读权限就代表能对此目录有列表功能，就是可以执行ls命令进行查看，另外还有cp的功能。

针对**文件**，有读权限就代表能对此文件有阅读功能，可以通过cat等命令查看文件内容。

- Write写权限表示：

针对**目录**，有写权限就代表着在此目录下创建文件和目录，可以通过touch，mkdir等命令创建文件和目录，另外还可以删除此目录下的文件。

针对**文件**，有写权限就代表着对此文件可以写入新的内容和修改文件内容。

- Execute执行权限表示：

针对**目录**，有执行权限就代表能进入此目录，利用cd等命令进入此目录。

针对**文件**，有执行权限就代表可以执行此文件。



#### 3. Linux文件与文件夹权限

##### 1. 文件与文件夹权限

在Linux中，可以使用umask查看当前用户的默认权限，创建文件/目录时会遵循该权限。

文件夹权限和文件权限的不同，会导致在使用命令操作文件时，有所不同。 

**文件权限**

对于文件而言，

-r表示文件的内容可以被读取

-w表示这个文件的内容可以被修改（w只授予文件修改的权限，如果需要删除/重命名，则需要有目录的w权限）

-x表示文件可以被执行，一般情况下，.sh文件需要有这个权限



**文件夹权限**

对于文件夹而言，

-r表示可以查看此文件夹下的文件名列表

-w表示可以对此文件夹下的文件进行删除/重命名/移动

-x表示可以将此文件夹作为working dir，或者说表示可以cd到这个文件夹中



**文件及文件夹权限实例**



![image-20210702101800090](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702101800090.png)



![image-20210702101814534](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702101814534.png)





##### 2. 修改文件权限



**chmod命令可以修改文件权限**

![image-20210702103324678](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702103324678.png)



##### 3. 文件的属组和属主



**chown命令可以修改文件的属主**



![image-20210702103619253](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702103619253.png)



**chgrp命令可以修改文件的属组**



![image-20210702104520997](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702104520997.png)



##### 4. 特殊权限

**SUID**

SUID是Set UID的简称，它会出现在文件拥有者权限的执行位上，具有这种权限的文件会在其执行时，使调用者暂时获得该文件拥有者的权限。

- **用个例子来了解SUID**

![image-20210702105147546](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702105147546.png)



- **SUID的使用需要满足以下四点**

1. SUID只对二进制文件有效
2. 调用者对该文件有执行权
3. 在执行过程中，调用者会暂时获得该文件的所有者权限
4. 该权限只在程序执行的过程中有效



**SGID**

SGID是Set GID的简称，它出现在文件所属组权限的执行位上面，它対普通二进制文件和目录都有效；

SGID作用于文件上时，在执行该文件时，用户将获得**该属组**的权限；

SGID作用于目录上时，**在该目录下创建的文件，都将属于这个目录所属的组。**



**SBIT**

SBIT即Sticky Bit，它出现在其他用户权限的执行位上，它只能用来修饰一个目录。

当某一个目录拥有SBIT权限时，则任何一个能够在这个目录下建立文件的用户，该用户在这个目录下所建立的文件，只有该用户自己和root可以删除，其他用户均不可以。



![image-20210702110400421](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702110400421.png)



**如何设置SUID，SGID，SBIT**

- **数字方式**

SUID，SGID，SBIT有自己对应的权限数字

SUID - 4

SGID - 2

SBIT - 1

设定权限只需要将对应的权限数字相加即可

在设置权限时，需要将特殊权限数字放在最前面，如果原文件权限为755，需要添加SUID权限，就执行 **chmod 4755 filename**



- **命令方式**

**chmod u+s testfile**     # 为**testfile文件**加上SUID权限

**chmod g+s testdir**      # 为**testdir目录**加上SGID权限

**chmod o+t testdir**      # 为**testdir目录**加上SBIT权限







## 服务管理

### 1. Linux下的init进程

#### 1. init进程

对于Linux系统的运行来说，init程序是最基本的程序之一。

一个好的Linux发行版本通常随带有一个init的配置，这个配置适合于绝大多数系统的工作，在这样一些系统上不需要对init做任何事。

通常，只有你在碰到诸如串行终端挂住了、拨入（不是拨出）调制解调器，或者你希望改变缺省的运行级别时才需要关心init。

init进程是所有Linux进程的父进程，它的进程号是1。



#### 2. init进程的实现

- **OpenRC**：OpenRC是一个基于依赖的init系统，它用C语言和遵循POSIX的shell写成，这使得它在BSD和Linux系统上可以使用。
- **Systemd**： Systemd是一套中央化系统及设置管理程序（init），其包括有守护进程、程序库以及应用程序。
- **Upstart**： Upstart是一个基于事件的init程序，用于替代传统的init（多种类Unix计算机操作系统启动时用于执行任务的程序）。
- **Sysvinit**： Sysvint就是system V风格的init系统，顾名思义，它源于System V系列Unix。它提供了比BSD风格init系统更高的灵活性。是已经风行了几十年的Unix int系统，一直被各类Linux发行版所采用。



### 2. Systemd

systemd服务是一种以.service结尾的单元（unit）配置文件，用于控制由systemd控制或监控的进程。简单说，用于后台以守护精灵（daemon）的形式运行程序。

systemd广泛应用于新版本的RHEL、SUSE Linux Enterprise、CentOS、Fedora和openSUSE中，用于替代旧有的服务管理器service。



##### 1. Systemd的常用命令

systemctl command xxx.service 		# 其中command可以是start、stop、restart、disable、enable等，比如：

systemctl start httpd.service 			# 启动Apache服务

systemctl enable mariadb.service 		# 将MariaDB服务设为开机启动



##### 2. 查看系统已有的Systemd配置文件

Systemd的配置文件都放置在/etc/systemd/system/ 目录下

![image-20210702120009261](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702120009261.png)



##### 3. Systemd配置文件

```shell
[Unit] # 这个项目与此unit的解释、执行服务相依性有关
Description=OpenBSD Secure Shell server
Documentation=man:sshd(8) man:sshd_config(5)
After=network.target audit.service
ConditionPathExists=!/etc/ssh/sshd_not_to_be_run

[Service]
EnvironmentFile=-/etc/default/ssh
ExecStartPre=/usr/sbin/sshd -t
ExecStart=/usr/sbin/sshd -D $SSHD_OPTS
ExecReload=/usr/sbin/sshd -t
ExecReload=/bin/kill -HUP $MAINPID
KillMode=process
Restart=on-failure
RestartPreventExitStatus=255
Type=notify
RuntimeDirectory=sshd
RuntimeDirectoryMode=0755

[Install]	# 这个项目说明此unit要挂载哪个target下面
WantedBy=multi-user.target
Alias=sshd.service

```



**Systemd的Unit**

在Systemd中，所有引导过程中systemd要控制的东西都是一个单元。基本的用法如下

- **Description**：代表整个单元的描述，可根据需要任意填写。
- **Wants**：本单元启动了，它“想要”的单元也会被启动。但是这个单元若启动不成功，对本单元没有影响。
- **Requires**：这个单元启动了，那么它“需要”的单元也会被启动；它“需要”的单元被停止了，它自己也活不了。但是请注意，这个设定并不能控制启动顺序，因为它“需要”的单元启动也需要时间，若它“需要”的单元启动还未完成，就开始启动本单元，则本单元也无法启动，所以不建议使用这个字段。
- **OnFailure**：若本单元启动失败了，那么这个单元作为折衷。
- **Befor/After**：指定启动顺序。



**Systemd的Service**

在定义完了Systemd用来识别服务的单元后，我们来定义服务本体。基本的用法如下：

- **Type**：服务的类型，各种类型的区别如下所示
  - **simple**：默认，这是最简单的服务类型。意思就是说启动的程序就是主体程序，这个程序要是退出那么一切皆休。
  - **forking**：标准Unix Daemon使用的启动方式。启动程序后会调用fork()函数，把必要的通信频道都设置好之后父进程退出，留下守护精灵的子进程。
  - **oneshot**：适用于那些被一次性执行的任务或者命令，它运行完成后便了无痕迹。因为这类服务运行完就没有任何痕迹，我们经常会需要使用RemainAfterExit=yes。意思是说，即使没有进程存在，Systemd也认为该服务启动成功了。同时只有这种类型支持多条命令，命令之间用；分割，如需换行可以用\。
  - **dbus**：这个程序启动时需要获取一块DBus空间，所以需要和BusName= 一起用。只有它成功获得了DBus空间，依赖它的程序才会被启动。
- **ExecStart**：在输入的命令是start时候执行的命令，这里的命令启动的程序必须使用绝对路径，比如你必须用/sbin/arp而不能简单的以环境变量直接使用arp。
- **ExecStop**：在输入的命令是stop时候执行的命令，要求同上。
- **ExecReload**：这个不是必需，如果不写则你的Service就不支持restart命令。ExecStart和ExecStop是必须有的。



**Systemd的Install**

服务编写完之后还需要被systemd装载，定义安装单元各个字段如下：

- **WantedBy**：设置服务被谁装载，一般设置为multi-user.target
- **Alias**：为service设置一个别名，可以使用多个名字来操作服务
- **Also**：在安装这个服务时候还需要其他的服务



**编写一个简单的systemd配置文件**

```shell
[root@m1 ~]# cd /etc/systemd/system
[root@m1 system]# vim alibaba.service

[Unit]
Description=Write Something
Wants=network-online.target
After=network.target

[Service]
Type=oneshot
RemainAfterExit=yes
ExecStart=touch /tmp/alibaba
ExecStop=rm -f /tmp/alibaba

[Install]
WantedBy=multi-user.target

[root@m1 system]# systemctl start alibaba.service			
[root@m1 system]# systemctl status alibaba.service				#此时/tmp目录下alibaba文件生成
● alibaba.service - Write Something
   Loaded: loaded (/etc/systemd/system/alibaba.service; disabled; vendor preset: disabled)
   Active: active (exited) since Fri 2021-07-02 15:48:47 CST; 1min 6s ago
  Process: 24765 ExecStart=/usr/bin/touch /tmp/alibaba (code=exited, status=0/SUCCESS)
 Main PID: 24765 (code=exited, status=0/SUCCESS)

Jul 02 15:48:47 m1 systemd[1]: Starting Write Something...
Jul 02 15:48:47 m1 systemd[1]: Started Write Something.

[root@m1 system]# systemctl stop alibaba.service 					#此时/tmp目录下alibaba文件被删除
```







### 3. CronTab定时任务

crontab是用来定期执行程序的命令。

当安装完成操作系统之后，默认便会启动此任务调度命令。

crond命令每分钟会定期检查是否有要执行的工作，如果有要执行的工作便会自动执行该工作。



#### 1. crontab常用命令介绍

- **crontab -l**	列出目前的日程表
- **crontab -e**   编辑当前日程表
- **crontab -r**   删除当前日程表
- **crontab -u xx -l**    列出xx用户的日程表



#### 2. crontab语法介绍

![image-20210702163101117](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702163101117.png)

![image-20210702163116607](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702163116607.png)

```shell
[root@m1 ~]# crontab -l
no crontab for root
[root@m1 ~]# crontab -e

* * * * * echo "123/r/n" >> /tmp/crontabtest

[root@m1 ~]# crontab -l
* * * * * echo "123/r/n" >> /tmp/crontabtest

[root@m1 ~]# systemctl restart crond.service
[root@m1 ~]# cd /tmp/
[root@m1 tmp]# ls
crontabtest  systemd-private-e656c944ad394e25b2303a9d994376a5-chronyd.service-vQyECi  vmware-root_869-3988752892
[root@m1 tmp]# more crontabtest
123/r/n
123/r/n
123/r/n
123/r/n
[root@m1 tmp]# crontab -r
[root@m1 tmp]# crontab -l
no crontab for root

```



#### 3. crontab的常用工具

[crontab.guru]()

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702164300012.png" alt="image-20210702164300012" style="zoom: 50%;" />



#### 4. crontab的注意事项

新创建的cron任务，不会马上执行，至少要过2分钟后才可以，当然你可以重启cron来马上执行。

crontab中的命令需要写成绝对路径。



### 4. Supervisor

Supervisor是用python开发的一套通用的进程管理程序，能将一个普通的命令行进程变成后台daemon，并监控进程状态，异常退出时能自动重启。

Supervisor可以很方便的管理批量进程，不仅支持启动、重启、关闭、重载，还支持监控进程，进程意外僵死后可自动拉起。



#### 1. Supervisor的安装

```shell
yum install -y epel-release
yum install -y supervisor
echo_supervisord_conf > /etc/supervisord.conf
supervisord -c /etc/supervisord.conf
```



#### 2. Supervisor配置管理

Supervisor的主进程配置文件放置在/etc/supervisord.conf

用户定义的项目进程配置文件放置在/etc/supervisord.d/conf.d目录下

```shell
[program:echo hi]
command=echo hi >> /tmp/hi
autostart=true
autorestart=true
startsecs=10
startretries=3
exitcode=0,2
stopsignal=QUIT
stopwaitsecs=10
user=root
log_stdout=true
log_stderr=true
logfile=/tmp/show_hi.log
logfile_maxbytes=1MB
logfile_backups=10
stdout_logfile_maxbytes=20MB
stdout_logfile_backups=20
stdout_logfile=/tmp/echo_hi.stdout.log
```





## 文本管理

### 1. 简单易用的编辑器 - Nano

#### 1. nano工具简介

GNU nano是一个小巧而友好的编辑器，除了基本的文本编辑功能以外，还提供了一些特色功能，如：redo/undo，交互式查找和替换自动缩进等功能。

**调用方式** 

nano filename



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702182528241.png" alt="image-20210702182528241" style="zoom: 45%;" />



Nano编辑器已经将过程中用到的快捷键在界面下方列出，其中，“^”一般表示“ctrl”键，“M”键一般表示“alt”键。

常用的快捷键如下：

- 保存	ctrl+o
- 读入    ctrl+r
- 帮助    ctrl+g
- 退出    ctrl+x
- 复制    atl+6
- 粘贴    ctrl+u



### 2. 强大的编辑器 - Vim

Vim是Vi improved的缩写。它是由Bram Moolenaar编写的免费开源文本编辑器。它于1991年首次发布，其主要目标是为Vi编辑器提供增强。与vi一样，它也是以命令为中心的编辑器。学习vim的一个好处是：它无处不在。如Linux、Mac、HP-UX、AIX等，Vim都是默认存在的。传统上vim没有GUI，但现在有一个GUI版本的gVim。

![image-20210702185554463](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702185554463.png)



#### 1. 优势

##### 高可配置性

使用一个简单的配置文件.vimrc。通过简单点的配置便可完成许多意想不到的任务。例如：可根据文件类型，使用不同的按键绑定等等

##### 高可扩展性

Vim支持插件扩展，如自动缩进，自动补全，目录等插件。曾有人将Vim打造成一个IDE。



#### 2. 命令模式、插入模式、可视模式及三者之间的切换

##### 命令模式

打开vim后的模式就是命令模式，在此模式下，几乎所有的按键按下后，屏幕上都不会显示，但可以进行复制、粘贴、删除等操作。当键入英文“：”后，界面的最下一行，便可以输入命令了。（：模式有时也叫命令行模式）

##### 插入模式

按下“i”或者“o”，可由命令模式转换为插入模式。按“Esc”键可返回命令模式。在插入模式下，便可像普通的编辑器那样进行输入了。（界面左下角会显示INSERT）

##### 可视模式

在命令模式下，按下“v”，可进入可视模式。按“Esc”键可返回命令模式。可视模式下移动光标，会以矩形框的形式选中内容，并可进行复制粘贴操作。（界面左下角会显示VISUAL）



#### 3. vim工具使用

##### 打开文件

可以在启动vim时，直接跟上需要的文件名。像这样：

```shell
vim filename
```

也可以这样，命令模式下输入：

```shell
:r filename
```

##### 退出

不保存文件，退出。如果文件未修改，直接“:q”。否则，需要":q!"。

```shell
:q!
```

保存退出

```shell
:wq
```

##### 复制

复制当前行，直接按键：

```shell
yy
```

从当前行开始，复制n行：

```shell
n yy
```

##### 粘贴

将光标移动到要粘贴的地方，内容将会粘贴到光标所在的下一行：

```shell
p
```

##### 删除

删除光标所在行：

```
dd
```

从当前行开始，删除n行：

```
n dd
```

##### 定位

使用命令显示行号：

```
:set nu
```

输入行号n，后跟G。可以跳到指定行：

```
nG
```

##### 查找

在命令模式下，/ 前向查找，？后向查找，后面跟上要查找的内容，回车确定：

```shell
/<expression>
```

查找下一个

```
n
```

查找上一个

```
N
```

##### Undo撤销操作

撤销上一个操作：

```
u
```

撤销上n个操作：

```
nu
```

##### Redo重做操作

直接使用ctrl -r 或者：

```
:red
```



### 3. 查找工具 - Grep

#### 1. 工具简介

Grep全称是Global Regular Expression Print。直译过来就是，全局正则表达式打印，顾名思义，此工具是通过使用**正则表达式**来匹配文件中的内容并将匹配到的内容打印出来。Grep工具有一系列变体，如fgrep，agrep，egrep等等。区别在于是否使用了正则表达式，和使用了哪种正则表达式集。

#### 2. 正则表达式

正则表达式实际上是一种模式，使用这种模式可以匹配对应的字符串集。正则表达式可以看做是一个有穷自动机。在Linux系统中的很多工具都使用到了正则表达式，比如之前我们讨论过的vim，和我们之后要讨论的sed和awk。

#### 3. Grep工具使用

##### 1. 命令行参数介绍

- **语法**

如下图所示，grep的命令行参数非常之多，在此，我们主要介绍如下使用方式：

```shell
grep [-e expression][filename]
```

-e		指定正则表达式

-i		不区别大小写

-n		显示行号

![image-20210702220509069](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210702220509069.png)



##### 2. 简单的正则表达式

- **"[]" 匹配指定字符集**

将匹配text1, text2, text3

```shell 
ls|grep -e 'text[123]'
text1
text2
text3
```

- **字符串精准匹配**

精确匹配"LINE"

```shell
grep -e 'LINE' .viminfo
```

- **"[^]" 不匹配指定字符集**

将不匹配text1, text2, text3, 输出text4, text5 

```shell
ls|grep -e 'text[^123]'
text4
text5
```

- **"*" 重复匹配**

将匹配t, to, too （*表示>=0个）

```shell
grep -e 'to*' text1
```

- **"+" 重复匹配**

将匹配to, too （+表示>0个）

```shell
grep -e 'to+' text1
```

- **"." 匹配任意单个字符**

将会输出文件全文

```shell
grep -e '.' .viminfo
```

- **"^" 头部匹配**

指明正则表达式必须是头部匹配，匹配所有text开头的字符串

```shell
grep -e '^text' text1
```

- **"$" 尾部匹配**

指明正则表达式必须是尾部匹配，匹配所有text结尾的字符串

```shell
grep -e 'text$' text1
```

- **转义字符**

经过前述的讨论可知，正则表达式中，使用了很多特殊字符，如"." "*" "[]" "^" "$" 等等还有很多没列出来的字符。加入要匹配的字符串中有这些符号，怎么办？

转义字符可以解决这个问题，转义字符是一个反斜杠"\\"

下列可以匹配以"$test$" 结尾的字符串

```shell
grep -e '\$test\$$' text1
```



##### 3. 正则表达式示例

- **C命名规范**

1. 变量名的开头必须是字母或下划线，不能是数字。
2. 变量名中的字母是区分大小写的。比如a和A是不同的变量名，num和Num也是不同的变量名。
3. 变量名绝对不可以是C语言关键字，这一点一定要记住。
4. 变量名是字母，数字，下划线的组合。

C变量示例：

```
[a-zA-Z_][a-zA-Z_0-9*]
```



##### 4. Grep常用场景

- **在文件中查找邮箱**

假设有这样一个场景，你有一个文件，像下图一样，数据量很大。你想知道该文件中是否存在某个人的邮箱，但你知道邮箱以.com结尾，并且邮箱中只含有字母和数字，要怎样才能减轻工作量呢？

![image-20210703112007608](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210703112007608.png)

可以先通过grep匹配出所有的以.com结尾邮箱

```shell
grep '[a-zA-Z0-9]\+@[a-zA-Z0-9]\+\.com>' log.txt
```

在将重复的进行筛选

```shell
grep '[a-zA-Z0-9]\+@[a-zA-Z0-9]\+\.com>' log.txt|uniq|sort
```



### 4. 流编辑器 - Sed

Sed的全称是Stream EDitor，它是一个简单而强大的文本解析转换工具，在1973-1974年期间由贝尔实验室的Lee E. McMahon开发，今天，它已经运行在所有的主流操作系统上了。

McMahon创建了一个通用的**行编辑器**，最终变成了Sed。Sed的很多语法和特性都借鉴了ed编辑器。设计之初，它就已经支持**正则表达式**，Sed可以从文件中接受类似于管道的输入，也可以接受来自标准输入流的输入。最强大地方是，内部实现里类似管道的处理方式。

Sed由自由软件基金组织（FSF）开发和维护并且随着GNU/Linux进行分发，因此，通常它也称作GNU Sed。对于新手来说，Sed的语法看起来可能有些神秘，但是，一旦掌握了它的语法，你就可以只用几行代码去解决非常复杂的任务，这就是Sed的魅力所在。

需要注意的是：Sed并**不会改变**源文件的内容。这是因为Sed内部维护了缓冲区的缘故，每次操作都是在缓冲区中的。

#### 1. 处理流程

![image-20210703114437269](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210703114437269.png)



#### 2. 命令

**命令的基本格式**

```shell
[address[,address]][!]action [arguments]
```

定位（address）和动作（action）

对于输入的每一行，检查是否符合第一个命令的定位信息。若满足，执行相应的动作，反之，不执行。接着检查第二个命令。在正常情况下，检查完脚本中的所有命令后，会将处理过的当前行输出。



#### 3. 定位

- **如何定位**

定位可以是行号。下例表示动作在第二行上执行：

```
2
```

定位也可以是正则表达式，用"/表达式/"表示，下例表示匹配所有空行：

```
/^$/
```

- **两个定位**

使用"," 隔开的两个位置。表示范围（闭区间）。下例表示动作在第二行到第六行都要执行：

```
2,6
```

第二行，到第一个空行

```
2,/^$/
```

- **最后一行**

使用"$" 表示



```shell
sed '2 p' test.txt		# 多打印文本第二行内容
sed -n '2 p' test.txt	# 只打印文本第二行内容
sed -n '2,5 p' test.txt		# 打印文本第二到第五行内容
```



#### 4. 几个主要动作

- **替换 s/pattern/replacement/flags**

pattern：匹配的正则表达式

replacement：替换字符串

flags：n第几次出现时执行

​			g	全局替换（替换每行中的所有）

​			p	打印

以下实例将 red替换成green

```shelll
s/red/green/5
s/red/green/g
s/red/green/p
```

- **打印**

打印2,6行

```
2,6p
```

- **删除**

删除2,6行

```
2,6d
```

- **插入**

插入到当前行之前，text为要插入的内容，定位只能有一个

[address]i text

示例，在第二行之前，插入

```shell
sed "2i This line is inserted by sed" text1 
```

- **追加**

插入到当前行之后，text为要插入的内容，定位只能有一个

[address]a text

示例，在第二行之后，插入

```shell
sed "2a This line is appended by sed" text1
```



#### 5. 语法

- **两种形式**

```shell
sed [-n]['command'][file...]	
sed [-n][-f scriptfile][file...]
```

- **-n**

只输出有p命令指定的行



#### 6. 批量替换

- **场景**

假设你有一个xml格式的数据集，存放的是地震的数据信息。但其中的日期格式是yyyy-mm-dd格式的。现在需要将其转换为mm/dd/yyyy格式。应该怎么做？只输出日期所在行呢？

- **结果**

```shell
sed -n 's/\([0-9]\{4\}\)-\([0-9]\{2\}\)-\([0-9]\{2\}\)/\2\/\3\/\1/p' sed-data.xml
```





### 5. 文本分析和处理 - Awk

#### 1. Awk工具简介

Awk是一种解析式编程语言，非常强大。是专门设计来进行文本处理的。名称是其三位创建者（Alfred Aho，Peter Weinberger，Brian Kernighan）姓的首字母。

GNU/Linux分发的版本是由自由软件基金会（FSF）维护的，常常被叫做Gawk。

Awk和Sed一样都是行编辑器。两者的工作流程很像，但Awk有很多更加强大的地方。

##### 1. 与sed相比的优点

- 方便的数值处理与计算
- 变量和流程控制
- 访问一行之中域
- 灵活的打印
- 内置数值和字符串函数
- 类C语法

##### 2. 脚本的结构

下图指出了一个awk程序/脚本的结构：

以BEGIN开始，以END结束。然而，这两个语句都是可选的。

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210704132807470.png" alt="image-20210704132807470" style="zoom:80%;" />

每一个命令都是一个pattern-action对，和sed类似。当输入符合模式时，对相应的action才会执行。如果省略pattern的话，则动作每一步都执行默认的动作是打印当前行

BEGIN - 读第一行之前执行

END - 处理完最后一行后执行



#### 2. 运行方式

##### 1. 第一种

awk 'script' input_files

此时的脚本内容通过命令行参数传进去

```shell
awk '{print}' text1
```



##### 2. 第二种

awk -f script_file input_file

将脚本文件传进去(awk1即为脚本)

```shell
awk -f awk1 text
```



#### 3. 工具使用

##### 1. 模式

- **正则表达式/pattern/**

将匹配text1, text2, text3

```shell
ls|awk '/text[123]/{print}'
```

- **！排除表达式**

不匹配text1, text2, text3

```shell
ls|awk '!/text[123]/{print}'
```

- **关系表达式**

超出一百字节的文件名

```shell
ls -l|awk '$5>100 {print $9}'
```

- **匹配表达式**

$9 == 'text1' 比较是否相等

$9 ~ /text*/ 是否和正则表达式匹配

下例匹配所有以text开头的文件

```shell
ls -l|awk '$9~/^text*/{print}'
```

- **多个表达式**

多个表达式之间，可以使用"||", "&&", 逻辑运算符

如找出大于100字节小于200字节，且以text为开头的文件，可以这样做：

```shell
ls -l|awk '$5>100 && $5<200 && $9~/^text*/{print $9}'
```



##### 2. 变量

- **可以定义和使用变量**

例如：

BEGIN{count = 0}

{ count++ }

END {print count}

**字符串变量初始化为null（即：\0）**

**数值变量初始化为0**

**变量不用声明**

awk中定义变量并不需要声明，awk会根据上下文环境，自动判断类型。

- **预定义变量**

前面提到过两个概念：行和域。这是粗略的类比。实际上在awk中有更精确的定义。

1. Record: 记录，默认为一行
2. RS(Record Separator): 记录分割符，默认为'\n'
3. NR(Number of Record): 指第几个记录
4. Field: 域
5. FS(Field Separator): 域分割符，默认是空白字符（一个或多个空格或tab）
6. NF(Number of Feild): 当前记录的域总数
7. 可通过 -F 或者在BEGIN action中指定，例如 FS=','
8. $0整个记录，$1表示第一个记录，$2表示第二个，以此类推

```shell
awk '
BEGIN{count=0 RS=''}
{count++}
END{print count}' text1
```

```shell
awk '
BEGIN{FS=','}
{print $0,$1}' text1
```



##### 3. 变量操作 - 字符串类型

- **字符串串接**

添加.txt后缀

```shell
{last = $0 ".txt"}
```

```shell
ls -l|awk '
$9 ~ /^text/{
last=$0 ".txt"
print last
}'
```

- **字符串赋值**

使用=直接赋值即可，如上例所示

```shell
{print $1,$2}
```

- **内置字符串函数**

内置了一系列字符串处理函数，如substr(str,s,n)。从str的第s位开始至多截取n个



##### 4. 输出

- **简单输出**

打印整个记录

```shell
{print}/{print $0}
```

- **使用变量**

打印第一个域

```shell
{print $1,$2}
```

使用字符串

```shell
{print "There are",NF,"fields"}
```

打印域总数

```shell
{print NF,$1,$NF}
```

添加行号（RS为'\n'时）

```shell
{print NR,$0}
```

##### 5. 输出printf

- **printf更为精细的输出控制**

像C一样，Awk允许使用，printf进行格式化输出。

```shell
printf(format,val1,val2,...)
```

示例：

```shell
ls -l|awk '{
string = "hello world"
printf("%10d %s\n",NR,string)
}'
```



#### 4. Awk常用场景

##### 统计各国的人口密度

![image-20210704152000933](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210704152000933.png)



```shell
awk '
BEGIN{
	printf("%10s %10s %8s %20s\n","国家","面积","人口/万人","人口密度 万人/km^2");
	printf("-------------------------------------------------------------\n");
	}
	{
	printf("%10s %10d %20f %20f\n",$2,$3,$4,$4/$3);
	area = area + $3;
	pop = pop + $4;
	}
END{
	printf("--------------------------------------------------------------\n");
	printf("%10s 面积 %12d km^2 %8f 万人 	\n\n","总共:",area, pop);
	printf("%10s %20f 万人/平方千米 \n\n", "平均人口密度: ",pop/area);
}'
```





## Shell脚本入门

### 1. 走进shell

#### 1. 什么是shell

Linux系统可划分为以下四个部分：

1. 应用软件
2. 窗口管理软件、
3. GNU系统工具链
4. Linux内核

![image-20210704181646332](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210704181646332.png)



#### 2. 如何使用shell

1. Linux shell是一种特殊的交互式工具，它提供了文件管理，运行进程的途径。
2. Shell的核心是命令提示符，允许用户输入命令，然后解释命令，并在内核中执行。
3. 用户可以编写脚本文件，将多个shell命令以某种形式组织起来，作为程序一起执行。



#### 3. 几种常见的shell

1. Shell有很多种，不同的shell有不同的特性
2. 几乎所有的Linux发行版默认shell是bash shell
3. 有些发行版的默认系统shell和默认交互shell并不相同
4. 查看系统支持的shell类型

```shell
cat /etc/shells
echo $SHELL
```



![image-20210704182122035](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210704182122035.png)



### 2. Shell常用命令

#### 1. Shell常用命令

##### 1. 管理文件和目录

-  cd	pwd	ls
- touch   cp   mv   rm
- mkdir   rmdir
- file   more   cat   less   tail   head

##### 2. 管理系统进程

- ps
- top
- kill   killall

##### 3. 管理磁盘空间

- mount   umount
- df
- dh

##### 4. 处理数据文件

- sort
- grep
- gzip   tar



#### 2. Shell外部命令

1. 外部命令（文件系统命令）通常位于/bin、/sbin、/usr/bin、/usr/sbin等目录
2. fork（复刻）：外部命令执行时，会创建出一个子进程。（以ps命令为例）

![image-20210704200905327](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210704200905327.png)



#### 3. Shell内建命令

1. 作为shell工具的组成部分，内建命令不需要使用子进程来执行
2. 对于有些命令，有多种实现，既有外部命令，也有内建命令
3. 了解某个命令的类型

```shell
type -a
```

4. 了解所有的内建命令

```shell
man builtin
```



### 3. Shell脚本基础

#### 1. 脚本创建、执行与退出状态码

##### 1. 创建shell脚本

Shebang(#!) 

```shell
#!/bin/bash
```

##### 2. 执行脚本

- 增加脚本的可执行权限
- 使用绝对或相对路径执行shell脚本

##### 3. 脚本的退出状态码

- 上一个命令的退出状态码

```shell
echo $?
```

- exit 命令



#### 2. 变量的定义与使用

##### 1. Linux系统的环境变量

- 全局环境变量
- 局部环境变量

##### 2. 自定义用户变量

- 由字母、数字、下划线组成
- 长度不超过20个字符
- 区分大小写

##### 3. 变量的定义/赋值

- 等号两边不能有空格

##### 4. 使用美元符号$对变量进行引用

- 建议使用${variable_name}

##### 5. 命令替换：将命令的输出赋值给变量

- 反引号'command'

- $(command)



```shell
#!/bin/bash

date
echo "current user is ${USER}"
echo "current user uid is ${UID}"
echo "current user home path is ${HOME}"
```

#### 3. 输出文本

##### 1. echo命令

注意下面三个的区别

```shell
[root@m1 ~]# echo $USER * $(date)
root anaconda-ks.cfg etcd-v3.2.12-linux-amd64 flanneld k8s kubernetes mk-docker-opts.sh README.md ssl test.sh Sun Jul 4 20:45:55 CST 2021
[root@m1 ~]# echo '$USER * $(date)'
$USER * $(date)
[root@m1 ~]# echo "$USER * $(date)"
root * Sun Jul  4 20:46:10 CST 2021
```



#### 4. 数字运算

##### 1. expr命令

```shell
[root@m1 ~]# expr 2 + 4
6
[root@m1 ~]# expr 2 \* 4
8
```

##### 2. $[operation]

```shell
[root@m1 ~]# echo $[2+4]
6
[root@m1 ~]# echo $[2*(3+4)]
14
```

##### 3. bc命令（支持浮点数运算）



### 4. Shell脚本控制条件

#### 1. if-then语句格式

```shell
 if  command
 then        
 	command
 fi  
```

##### 1. 当if后面的命令，运行后的退出状态码是0时（命令执行成功），then后面的命令会被执行。

##### 2. if-then语句扩展

if-then-elif-else语句格式

```shell
if	command1
then
	commandA
elif	
	command2
then	
	commandB
elif	
	command3
then	
	commandC
else
	commandD
fi
```

##### 3. 条件测试

1. test命令提供了在if-then语句中测试不同条件的途径。
2. 如果test命令中列出的条件成立，返回的退出状态码为0，反之为1.
3. test命令的等价写法 []

```shell
if test condition
then
	commands
fi
```

```shell
if [condition]
then
	commands
fi
```

提供的三类判断条件

- 数值比较
- 字符串比较
- 文件比较

##### 4. test命令的数值比较

![image-20210705101626104](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210705101626104.png)

##### 5. test命令的字符串比较

![image-20210705101754095](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210705101754095.png)

##### 6. test命令的文件比较

![image-20210705103018492](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210705103018492.png)

##### 7. 复合条件测试

使用布尔运算符

1. [condition 1] && [condition 2]

2. [condition 1] || [condition 2]

##### 8. if-then语句高级特性

- **双括号** **(())**

1. 支持高级数学表达式的计算

2. 命令格式：((expression))

3. expression可以是数学赋值或比较表达式

示例：

```shell
#!/bin/bash

value=10
if (( ${value} ** 2 > 90 ))
then
	(( answer = ${value} ** 2 ))
	echo "The square of ${value} is ${answer}"
fi
```

- **双方括号 [[]]**

1. 支持针对字符串比较的高级特性
2. 命令格式：[[expression]]

3. 除了标准的字符串比较，还支持模式匹配

示例：

```shell
#!/bin/bash

if [[ ${USER} == r* ]]
then 
	echo "Hello ${USER}"
fi
```



#### 2. case语句

常代替if-then-elif语句用于对某个变量有大量判断语句的场景。

```shell
case expression in 
	pattern1)
		commands;;
	pattern2)
		commands;;
	pattern3 | pattern4)
		commands;;
	*)
		default commands;;
esac
```

示例：

```shell
case ${USER} in
	mysql)
		echo "current user is mysql.";;
	root)
		echo "current user is root.";;
	*)
		echo "unknown user.";;
esac
```



### 5. Shell脚本循环控制

#### 1. for语句

1. 用于遍历一个指定的列表，每次迭代使用列表中的一个元素，执行定义好的一组命令
2. for语句格式：

```shell
for var in list
do 
	commands
done
```

```shell
for var in list;do
	commands
done
```

##### 1. for语句使用示例

1. **读取列表中的值**

```shell
#!/bin/bash

for fruit in apple lemon orange
do
	echo "This is $fruit"
done
	echo "The last is $fruit"
```

输出

```shell
This is apple
This is lemon
This is orange
The last is orange
```

2. **读取列表中的复杂值**

```shell
#!/bin/bash

for word in I don\'t know whether "it's" good "or not"
do 
	echo "word: ${word}"
done
```

输出

```
word: I
word: don't
word: know
word: whether
word: it's
word: good
word: or not
```

3. **从变量读取列表**

```shell
#!/bin/bash

fruits="apple lemon orange"
for	fruit in $fruits
do
	echo "This is $fruit"
done
```

输出

```
This is apple
This is lemon
This is orange
```

4. **从命令读取值**

```shell
#!/bin/bash

file="fruitlist.txt"
for fruit in $(cat ${file})
do
	echo "This is $fruit"
done
```

输出

```
This is apple
This is lemon
This is orange
```

5. **更改字段分隔符 $IFS**

```shell
#!/bin/bash

fruits="apple:lemon:orange"
IFS=:
for fruit in $fruits
do
	echo "This is $fruit"
done
```

输出

```
This is apple
This is lemon
This is orange
```

6. **用通配符遍历目录**

```shell
#!/bin/bash

for file in /tmp/*
do
	if [ -f $file ]
	then
		echo "file: $file"
	elif [ -d $file ]
	then
		echo "directory: $file"
	fi
done
```

输出

````
file: /tmp/crontabtest
file: /tmp/supervisord.log
file: /tmp/supervisord.pid
directory: /tmp/systemd-private-e656c944ad394e25b2303a9d994376a5-chronyd.service-vQyECi
directory: /tmp/vmware-root_869-3988752892
````



#### 2. for语句（C语言风格）

1. 变量赋值的两边可以有空格
2. 条件中的变量可以不以$符开头
3. 迭代过程的表达式可以不用expr命令格式

**不建议使用**

```shell
for (( 变量赋值；迭代条件；迭代过程 ))
do
	commands
done
```

```shell
#!/bin/bash

for (( i=1;i<=10;i++ ))
do 
	echo "The number is $i"
done
```



#### 3. while/until语句

- **while**

```shell
while test command
do
	other commands
done
```

```shell
#!/bin/bash
i=1
while [ $i -le 10 ]
do 
	echo "The number is $i"
	(( i = i + 1 ))
done
```

- **until**

```shell
until test command
do
	other commands
done
```

```shell
#!/bin/bash
i=1
until [ $i -gt 10 ]
do 
	echo "The number is $i"
	(( i = i + 1 ))
done
```



#### 4. 循环控制语句 - break

break可以退出任意类型的循环

1. 跳出内部循环
2. 跳出外部循环 break n

```shell
#!/bin/bash

for i in $(seq 1 9)
do
	for j in $(seq 1 9)
	do
		if [ $j -gt 3 ];then
			break
		else
			echo "$i * $j = $(( i * j ))"
		fi
	done
done
```



#### 5. 循环控制语句

1. continue可以跳过执行当前循环的命令，但不会终止整个循环
2. 可指定跳过的循环层数 continue n



### 6. Shell处理简单输入

#### 1. 命令行参数

1. 命令行参数：向shell脚本传递数据最基本的方法
2. 位置参数：$0是脚本名，$1到$9表示第一到第九个参数，第十个参数可以用${10}表示
3. 若参数内容包含空格，则必须使用引号

##### 示例

1. 例：计算两个数之和

```shell
#!/bin/bash

result=$[ $1 + $2 ]

echo "the first parameter is $1"
echo "the second parameter is $2"
echo "the answer is $result"

[root@m1 ~]# ./test.sh 10 20
the first parameter is 10
the second parameter is 20
the answer is 30
```

2. 计算前需要检查参数是否存在数据

```shell
#!/bin/bash

if [ -n "$1" ] && [ -n "$2" ];then	
	result=$[ $1 + $2 ]
	echo "the first parameter is $1"
	echo "the second parameter is $2"
	echo "the answer is $result"
else
	echo "the script needs two parameters."
fi
[root@m1 ~]# ./test.sh 10
the script needs two parameters.
```

#### 2. 特殊参数变量 - $#

$#存储了脚本运行时携带的命令行参数的个数

与上例同理

```shell
#!/bin/bash

if [ $# -eq 2 ];then
	result=$[ $1 + $2 ]
	echo "the first parameter is $1"
	echo "the second parameter is $2"
	echo "the answer is $result"
else
	echo "the script needs two parameters."
fi
[root@m1 ~]# ./test.sh 10
the script needs two parameters.
```



#### 3. 特殊参数变量 - $*, $@

1. $*和$@能够在单个变量中存储所有命令行参数
2. 区别在于$*是一个整体，$@是多个个体

#### 4. 移动变量

1. shift命令可以将每个参数变量向左移动一个位置
2. 常用于遍历命令行参数
3. shift n

```shell
#!/bin/bash

count=1
while [ -n "$1" ]
do
	echo "#${count}. Hello, $1"
	count=$[ $count + 1 ]
	shift
done

[root@m1 ~]# ./test.sh Alich Bob James Axe
#1. Hello, Alich
#2. Hello, Bob
#3. Hello, James
#4. Hello, Axe
```

#### 5. 交互式处理 - read命令

1. 从标准输入读取数据并赋值给指定变量

- 指定输出的命令行提示信息（-p）
- 指定接收单字符的数据（-n）
- 设置输入的超时时间（-t）

2. 从文件中读取参数

```shell
#!/bin/bash

read -p "Enter your name:" first last

echo "Your first name is ${first}"
echo "Your last name is ${last}"

[root@m1 ~]# ./test.sh
Enter your name:Axe wang
Your first name is Axe
Your last name is wang
```

```shell
#!/bin/bash

read -n -p "Do you want to continue[Y/N]?" ans

echo 
case $ans in
	Y|y)
		echo "yes";;
	N|n)
		echo "Bye";;
esac

[root@m1 ~]# ./test.sh
Do you want to continue[Y/N]?n
Bye
```

```shell
#!/bin/bash

if read -t 5 -p "Enter your answer: " num
then 
	echo "Your answer is ${num}"
else
	echo
	echo "Sorry, timeout!"
fi

[root@m1 ~]# ./test.sh
Enter your answer: 36
Your answer is 36
```

```shell
#!/bin/bash

filename="data.txt"
if [ -f ${filename} ]; then
	count=1;
	cat data.txt | while read line
	do 
		echo "Line ${count}: ${line}"
		count=$[ $count + 1 ]
	done
	echo "Finished reading the file"
else
	echo "${filename} is not found!"
fi

[root@m1 ~]# ./test.sh
Line 1: BattleField
Line 2: Horized
Line 3: Monster Hunter
Line 4: GTA
Finished reading the file
```



#### 6. Shell脚本重定向

##### 1. 标准文件描述符

Linux用标准文件描述符来标识每个文件对象

![image-20210705231259174](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210705231259174.png)

##### 2. 重定向错误输出

1. 只重定向错误输出

```shell
ls -al badfile 2> error.log
```

2. 重定向错误和普通输出

```shell
ls -al badfile testfile 2> error.log 1> output.log
```

3. 重定向错误和普通输出到同一文件

```shell
ls -al badfile testfile &> output.log
```

##### 3. 在脚本中重定向输出

1. **临时重定向**

重定向到文件描述符时，必须在文件描述符数字前加一个&

```shell
echo "This is a error message" >&2
```

```shell
#!/bin/bash

echo "This is a error message" >&2
echo "This is a normal message"

[root@m1 ~]# ./test.sh 2> error.log
This is a normal message
[root@m1 ~]# cat error.log
This is a error message
```

2. **永久重定向**

- 使用exec命令在脚本执行期间重定向某个特定文件描述符
- exec命令会启动一个shell来进行数据重定向

```shell
#!/bin/bash

exec 1> output.tst
echo "This is a normal message"

[root@m1 ~]# ./test.sh
[root@m1 ~]# cat output.tst
This is a normal message
```

##### 4. 创建自己的重定向

1. 创建文件描述符

```shell
exec 3> output_file
exec 0> input_file
exec 6<> test_file
```

2. 关闭文件描述符

```shell
exec 6>&-
exec 6>&-
```

3. 实现一个简单的线程池

- 脚本需要并发的执行任务
- 令牌桶模型控制并发数

```shell
#!/bin/bash

n_thread=3
tmp_fifofile="script.fifo"
rm -rf ${tmp_fifofile}

mkfifo ${tmp_fifofile}
exec 6<> ${tmp_fifofile}

for (( i = 1; i <= ${n_thread}; i++ )); do
	echo >&6
done

for i in $(seq 100 200); do
	read -u6
	{
		echo "thread handling number:${i}"
		sleep 3
		echo >&6
	} &
done

wait

rm ${tmp_fifofile}
exec 6>&-
exec 6<&-
```



### 7. Shell脚本函数

#### 1. 基本的脚本函数

##### 1. 创建函数

- function func_name {...}
- func_name() {...}

##### 2. 使用函数

- func_name

#### 2. 在函数中使用变量

##### 1. 向函数传递参数

- 位置参数变量

##### 2. 在函数中处理变量

- 全局变量
- 局部变量local

#### 3. 函数的返回值

##### 1. 默认的退出状态码

- $?

##### 2. 使用return命令

- 整数0-255

##### 3. 使用命令执行获取函数输出

- ans=${func}



### 8. Shell脚本简单实例

获取指定目录中占用空间大小前十的子目录，并生成每日报告

##### 1. 核心命令

```shell
du -S [directory]
sort -n
```

##### 2. 核心功能

准备需要检测的目录，得到（子）目录统计数据，将结果生成每日报告

##### 3. 完善脚本

执行验证，设置计划任务



