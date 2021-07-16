## Linux基本知识

### 1. Linux基本介绍

#### Linux是什么

Linux是一种自由的开放源代码的类Unix操作系统

#### Linux的诞生过程

Unix操作系统是由贝尔实验室于1969年开发的一个操作系统，最初由汇编语言实现，在1973年的时候用C语言重写，更加方便移植到不同的平台上去。开始Unix是以免费许可证授权给学术机构的，因此百花齐放，形成了很多Unix变种操作系统。但是后来贝尔实验室意识到商业价值不再授权给学术机构，这催生了Minix。

Linux则是由linus torvalds在1991年赫尔辛基大学上学时，出于对操作系统的好奇而开发的，起初他在他购买的计算机上安装minix，但是后来他逐渐为自己的计算机写了很多驱动程序，也认识到了minix作为一个教学用的操作系统有许多不足，然后逐步形成了Linux操作系统。

#### Linux内核与Linux内核发行版

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210628204914566.png" alt="image-20210628204914566" style="zoom: 67%;" />

#### 常见的Linux发行版

Ubuntu、Debian、RHEL、Centos、Fedora、Arch、Gentoo等



### 2. Linux基础安全介绍

#### SSH登录方式介绍

SSH全称为Secure Shell，是一种加密的网络传输协议。可以创建安全的隧道用于客户端与服务器连接，可以使用非对称加密做验证。

#### SSH基本安全配置

实操生成密钥，与配置ssh

```shell
ssh-keygen # 生成密钥

vim /etc/ssh/sshd_config 
```





### 3. Linux文件管理

#### Linux系统目录结构FHS介绍

FHS全称Filesystem Hierarchy Standard，中文名文件系统结构层次，定义了Linux操作系统中的主要目录和目录结构。 FHS由Linux基金会维护，当前当前版本是3.0

![image-20210628200913315](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210628200913315.png)



![image-20210628201031959](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210628201031959.png)



#### 操作文件的几个常用命令

Linux中一切皆文件

![image-20210628201548220](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210628201548220.png)

#### 简单介绍man系统

man系统其实是linux中的manual手册系统，大多数程序会自带手册，所以当一个命令不会使用的时候不妨查查手册

![image-20210628202220356](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210628202220356.png)

### 4. Linux服务与日志

#### 服务的基本概念

服务的英文名是service，服务顾名思义就是能为系统或者用户提供某种特定服务的程序。

只不过这种程序一般是在后台常驻，不是我们直接运行，这种程序一般叫守护进程daemon。



常见的服务有

- SSH，用于我们随时能连接到服务器，提供这个服务的程序是sshd
- cron，提供定时任务的服务，提供这个服务的程序是crond



#### 常见的服务管理方式

systemd是一种init程序，用于初始化系统，提供了对服务的管理方式。

![image-20210628203105760](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210628203105760.png)

#### 日志与日志的查询方式

日志是由程序在运行过程中打印出来的一些执行流程或者记录信息的文本。

systemd同样也提供了对日志访问的方式

![image-20210628203435754](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210628203435754.png)





通过直接查看文本的方式查询

![image-20210628203629124](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210628203629124.png)







## 操作系统学习

### 1. Debian系

#### Debian

![image-20210701154933922](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701154933922.png)

#### Ubuntu

![image-20210701155050509](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701155050509.png)





### 2. RHEL系

#### RHEL(Red Hat Enterprise Linux)

![image-20210701155526762](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701155526762.png)



#### Fedora

![image-20210701155623150](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701155623150.png)



#### Centos

![image-20210701155720005](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701155720005.png)



#### Anolis OS

![image-20210701155909953](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701155909953.png)



### 3. LFS以及其他的发行版本

#### Arch Linux

![image-20210701160017013](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701160017013.png)



#### Gentoo Linux

![image-20210701160137356](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701160137356.png)



#### Linux from scratch

![image-20210701160339109](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701160339109.png)



## 服务器硬件基础

### 1. 服务器的核心硬件

#### 1. 内部硬件

服务器和普通的PC一样，核心的硬件主要是以下四大件-

- **CPU**：决定当前服务器的计算能力上限
- **内存**：决定当前服务器同时传递信息的上限
- **硬盘**：决定当前服务器能够存储信息的上限
- **网卡**：网卡决定了服务器与外部沟通时传递信息的效率

#### 2. 外部硬件

服务器除了内部硬件以外，还涉及到大量的外部硬件，以确保服务器的正常运转-

- **网络系统**：服务器在机房工作时，会面临复杂的网络环境，这时需要一个复杂的网络系统协助服务器工作
- **监控系统**：服务器在运转过程中可能出现各种意外情况，一个监控系统可以帮助网络工程师快速发现服务器的异常
- **控温系统**：在服务器运转过程中会产生大量的热量，控温系统可以确保服务器的运行环境温度保持常温，避免高温缩短服务器寿命
- **供电系统**：机房也存在出现电力故障的情况，一套供电系统可以在出现电力系统故障的时候，持续支持服务器正常运转，正常关机
- ...



### 2. 服务器的历史演变

#### 1. 服务器的发展历史

**1946-1954 电子管时代**

![image-20210701162949062](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701162949062.png)



**1954-1964 晶体管时代**



![image-20210701163125947](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701163125947.png)

![image-20210701163201995](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701163201995.png)

**1970年至今**



![image-20210701163238251](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701163238251.png)

![image-20210701163248308](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701163248308.png)



#### 2. 企业使用服务器的历史

![image-20210701163433683](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701163433683.png)

- 计算机是由大型机开始，逐渐变小、运算能力变强，走入寻常百姓家
- 企业/个人使用服务器的成本逐渐降低
- 目前使用的云服务器，便是经过历史考验后，当下能够实现最轻量，最易用的服务器方案



### 3. 云服务器与裸金属服务器

#### 1. 云服务器的优势和应用场景

云服务器免去了采购IT硬件的前期准备，让用户像使用水、电、天然气等公共资源一样便捷、高效的使用服务器，实现计算资源的即开即用和弹性伸缩。持续提供创新型服务器，解决多种业务需求，助力业务的发展。

**云服务器的优势**

- **高可用性**：相较于普通的IDC机房以及服务器厂商，云服务器会使用更严格的IDC标准、服务器准入标准以及运维标准，保证云计算框架的高可用性、数据的可靠性以及云服务器的高可用性。
- **安全性**：云计算提供了诸如VPC、专线互联、私有云等解决方案，更加安全稳定。
- **弹性**：云服务器提供了纵向与横向的弹性能力，可以保障业务量暴增而产生的资源需求。



![image-20210701165151456](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701165151456.png)



**云服务器的应用场景**

- 企业官网或轻量化的Web应用
- 多媒体以及高并发应用或网站
- 高I/O要求数据库
- 访问量波动剧烈的应用或网站
- 大数据及实时在线或离线分析
- 机器学习和深度学习等AI应用
- ...



#### 2. 裸金属服务器的优势和应用场景

裸金属服务器（Bare Metal Server）类似云上的专属物理服务器，在拥有弹性灵活的基础上，具有高性能的计算能力。计算性能与传统物理机无差别，具有安全物理隔离的特点。

弹性裸金属服务器（ECS Bare Metal Instance）是基于下一代虚拟化技术而打造的新型计算机类服务器产品，兼具虚拟机的弹性和物理机的性能及功能特性。与上一代虚拟化技术相比，下一代虚拟化技术不仅保留了普通云服务器的弹性体验，而且保留了物理机的性能与特性，全面支持嵌套虚拟化技术。

弹性裸金属服务器融合了物理机与云服务器的优势，实现超强超稳的计算能力。通过阿里云自主研发的虚拟化2.0技术，**用户的业务应用可以直接访问弹性裸金属服务器的处理器和内存，无任何虚拟化开销。弹性裸金属服务器具备物理机级别的完整处理器特性（例如Intel VT-x），以及物理机级别的资源隔离优势，特别适合上云部署传统非虚拟化场景的应用。**



 **裸金属服务器的优势**

- **用户独占计算资源**

作为一款云端弹性计算类产品，弹性裸金属服务器具备了物理机级的性能和隔离性。用户可以独占计算资源，并且没有虚拟化性能开销和特性损失。在CPU规格选择上支持8核，32核，80核，96核，104核等多个规格，并支持超高主频实例。

- **加密计算**

在安全性方面，弹性裸金属服务器除了具备物理隔离特性外，为了更好的保障云上数据的安全性，弹性裸金属服务器采用了芯片级可信执行环境（Intel@SGX），能确保加密数据只能在安全可信的环境中计算。

- **兼容多种专有云**

弹性裸金属服务器可以进一步解决用户对高性能计算的强需求，更好的帮助用户搭建新型混合云，弹性裸金属服务器不仅具有虚拟机的灵活性和弹性，同时具备物理机的一切特性和优势，因此也具备再次虚拟化的能力，线下的私有云均可无缝平移到云服务器上，而不用担心嵌套虚拟化带来的性能开销，为用户上云提供一种新途径。

- **异构指令集处理器支持**



 **裸金属服务器应用场景**

- **对安全和监管高要求的场景**

金融、证券等行业对业务部署的合规性，以及某些客户对数据安全有苛刻的要求。采用裸金属服务器部署，能够确保资源独享、数据隔离、可监管可追溯。

- **高性能计算场景**

超算中心、基因测序等高性能计算场景，处理的数据量大，对服务器的计算性能、稳定性、实时性等要求很高，裸金属服务器可以满足高性能计算的需求。

- **核心数据库场景**

某些关键的数据库业务不能部署在虚拟机上，必须通过资源专享、网络隔离、性能有保障的物理服务器承载。裸金属服务器为用户提供独享的高性能的物理服务器，可以满足此种场景下的业务需求。

- **移动应用场景**

围绕移动应用尤其是手机游戏的开发、测试、上线、运营，借助鲲鹏系列服务器对终端设备的兼容性优势，以鲲鹏系列裸金属服务器为基础打造一站式整体解决方案。



**裸金属服务器与传统IDC对比**

![image-20210701173543052](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210701173543052.png)



