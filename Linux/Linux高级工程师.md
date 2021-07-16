# HTTP服务

## 高性能集群负载







# 虚拟化

## KVM虚拟化

### 1. KVM虚拟化

#### 1. 虚拟化与云计算

##### 云计算的发展

云计算于2006年，首次被 Google 前首席执行官 Eric Schmidt 提出。

在20世纪60年代，麦卡锡（John McCarthy）就提出了把计算能力作为一种像水和电一样的公用事业提供给用户。

在20世纪90年代，网格计算的诞生让人们看到了云计算的雏形。

##### 云计算与虚拟化

云计算的云端系统，其实质上就是一个大型的分布式系统。

虚拟化通过在一个物理平台上虚拟出更多的虚拟平台，而其中的每一个虚拟平台则可以作为独立的终端加入云端的分布式系统。

比起直接使用物理平台，虚拟化在资源的有效利用、动态调配和高可靠性方面有着巨大的优势。

利用虚拟化，企业不必抛弃现有的基础架构即可构建全新的信息基础架构，从而更加充分利用原有的IT投资。

##### 何为虚拟化

我们可以将一般的计算模型抽象成为一定的物理资源和运行于之上的计算元件，它们之间通过定义的物理资源接口进行交互。

随着计算机硬件技术的发展，物理资源的容量越来越大而价格越来越低，在既有的计算元件架构下，物理资源不可避免的产生了闲置和浪费。

为了充分利用新的物理资源，提高效率，一个比较直接的办法就是更新计算元件以利用更加丰富的物理资源。

但是，人们往往出于对稳定性和兼容性的追求，并不情愿频繁地对已经存在的计算元件做大幅度的变更。

虚拟化技术则是另辟蹊径，通过引入一个新的虚拟化层，对下管理真实的物理资源，对上提供虚拟的系统资源，从而实现了在扩大硬件容量的同时，简化软件的重新配置过程。

#### 2. 不同的虚拟化

- 服务器虚拟化
- 网络虚拟化
- 桌面虚拟化
- 软件定义存储

#### 3. 软件虚拟化与硬件虚拟化

纯软件虚拟化，是用纯软件的方法在现有的物理平台上（往往不支持硬件虚拟化）实现对物理平台访问的截获和模拟。

常见的软件虚拟机例如QWMU、VMWare、VirtualBox等

硬件虚拟化，是物理平台本身提供了对特殊指令的截获和重定向的硬件支持。甚至，新的硬件会提供额外的资源来帮助软件实现对关键硬件资源的虚拟化，从而提升性能。

#### 4. 全虚拟化与半虚拟化

软件虚拟化可以在缺乏硬件虚拟化支持的平台上完全通过VMM软件来实现对各个虚拟机的监控，以保证它们之间彼此独立和隔离。但是付出的代价是软件复杂度的增加，和性能上的缺失。

半虚拟化是通过修改操作系统，使它以为自己运行在虚拟环境下，能够与虚拟机监控机协同工作。

全虚拟化为客户机提供了完整的虚拟X86平台，包括处理器、内存和外设，支持运行任何理论上可在真实物理平台上运行的操作系统，为虚拟机的配置提供了最大程度的灵活性。



### 2. 配置KVM

#### 1. KVM虚拟化

KVM是基于内核的虚拟机（Kernel-based Virtual Machine）的缩写。

KVM是为Linux环境而设计的虚拟化基础设施，后来移植到FreeBSD和IIIumos。

KVM支持硬件辅助的虚拟化技术（即能够充分利用硬件厂商提供的硬件虚拟化机制），其一开始支持的架构为Intel公司的X86和X86-64处理器，后来则被IBM公司移植到S/390、PowerPC和IA-6L。

KVM虚拟机监视器既可以在全虚拟化模式下运行，也能够为部分操作系统提供准虚拟化支持。在准虚拟化模式下，KVM使用一种称为VirtIO的框架作为后端驱动。该框架能够支持准虚拟化的以太网卡、准虚拟化的控制器，调整宿主内存容量的设备，以及使用 SPICE 或 VMWare 驱动程序的VGA图形界面。

#### 2. Xen虚拟化

Xen虚拟机技术是英国剑桥大学计算机实验室原始开发的。

Xen社区负责Xen的后续版本开发并将其作为免费开源的软件，以GNU通用公众执照（GeneralPublic License）（GPLv2）进行使用。

著名的亚马逊Web服务（AWS）就建立于Xen虚拟机技术上。

Xen虚拟机的最大商用支持者为美国的Citrix公司。

#### 3. Hyper-V虚拟化

Hyper-V是微软公司使用的虚拟机监视器，其前身是 Windows 服务器虚拟化（Windows Server Virtualization）。

Hyper-V提供的虚拟机容器称为划分，其中根划分里面容纳的是主机操作系统，自划分里面则运行宿主操作系统。宿主操作系统可以是非Windows操作系统。

所有的划分之间由虚拟总线进行连接，不同的主机或宿主操作系统之间的通信均通过该总线进行。

目前，Hyper-V的使用者主要是微软的Windows Azure。

#### 4. Container容器技术

Container技术利用了Linux kernel提供的cgroup、namespace等机制，将应用之间隔离起来，好像自己是操作系统上的唯一一个应用似的。

与平台虚拟化技术想比，Container技术省去了启动和维护整个虚拟客户机的开销（硬件初始化、Kernel boot、init等），因而它非常轻量级，非常适用于Paas服务模型。

但另一方面，由于各个Contained instance其实还是公用一个OS、一个Kernel，所以安全性比不上平台虚拟化技术。总而言之，Container和KVM等平台虚拟化技术，目前还是各有所长，还处在相互取长补短的过程中。

#### 5. 配置KVM

```bash
egep -c '(vmx|svm)' /proc/cpuinfo	# 查看OS是否支持虚拟化
kvm-ok								# 查看OS是否支持虚拟化
sudo apt install qemu-kvm libvirt-daemon-system libvirt-clients bridge-utils
sudo systemctl start libvirtd.service
sudo systemctl enable libvirtd.service
sudo adduser axe libvirt
sudo adduser axe kvm
virsh list --all					# 验证是否配置成功
sudo systemctl status libvirtd.service		# 验证是否配置成功
sudo apt install virt-manager
sudo virt-manager
```



### 3. 管理KVM虚拟机

#### 1. 管理KVM虚拟机的一个核心命令

- virtsh - 命令行下的虚拟机管理工具
- virt-manager - 可视化管理工具
- virt-viewer - 虚拟机查看工具
- virt-install - 命令行下的虚拟机创建命令

#### 2. 虚拟机核心资源

在之前的内容中介绍过，虚拟机最核心的便是将硬件资源放置在资源池内重新分配

在 libvirt 中，最为核心的便是对硬件资源的虚拟化：CPU、存储、网络

#### 3. 存储池 Storage Pool

在 libvirt 中，最核心的是 Storage Pool

Storage Pool 将存储归纳整理成为一个个不同的 Storage Pool

Storage Pool 可以跨越不同的硬件，如，一个 Storage Pool 可以由多个硬件组成

##### 存储池管理

```bash
virsh pool-list --all			# 查看所有存储池
virsh pool-define-as poolname dir - - - - /home/username/.local/libvirt/images		# 定义一个新的存储池
virsh pool-build poolname		# 构建存储池
virsh pool-strat poolname		# 启用存储池
virsh pool-autostart poolname	# 自启动存储池
virsh pool-undefine poolname	# 删除存储池
```

```bash
virsh pool-define-as vdisk dir --target /home/user/virtdisk	# 定义存储池挂载点
irsh pool-build vdisk						# 构建存储池
virsh pool-start vdisk						# 启动存储池
virsh pool-autostart vdisk					# 设置存储池开机自启动
```



#### 4. 存储卷 Storage Volume

存储池被创建之后，就可以在存储池中创建存储卷。

存储卷是实际用来存储数据的单位

存储卷有明确的大小的限制

##### 存储卷管理

```bash
virsh vol-create-as	poolname volumename 10GiB --format aw|bochs|raw|qcow|qcow2|vmdk
virsh vol-upload --pool poolname volumename volumepath
virsh vol-list	poolname
virsh vol-resize --pool poolname volumename 12GiB
virsh vol-delete --pool poolname volumename
virsh vol-dumpxml --pool poolname volumename	# 查看详情
```

```bash
vol-create-as vdisk datafile 150MiB --format qcow2	# 创建存储卷
vol-list vdisk										# 查看存储卷
vol-info datafile --pool vdisk						# 查看存储卷信息
vol-resize datafile 155MiB --pool vdisk				# 修改存储卷大小
```



#### 5. 虚拟机domain

在libvirt中，每一个虚拟机都被称为 Domain，我们对于虚拟机的操作，实际上是对于 Domain 的操作。

##### 管理虚拟化

```bash
virsh list --all	# 查看所有虚拟机
virt-install --name debian --memory 1024 --vcpus=2,maxvcpus=4 --cpu host --cdrom $HOME/iso/debian.iso --disk size=2,format=raw --network user --virt-type kvm	# 创建虚拟机
vir-install --name demo --memory 512 --disk /home/user/VMs/mydisk.img --import	# 导入创建好的虚拟机
virsh start domain	# 启动虚拟机
virsh shutdown domain			# 关闭虚拟机
virsh edit domain	# 编辑虚拟机
```

```bash
virt-install --name centos --memory 512 --vcpus=1,maxvcpus=1 --cpu host --cdrom /home/gothizzz/CentOS-7-x86_64-Minimal-2009.iso --disk size=3.5,format=qcow2 --network user --virt-type kvm
```



#### 6. 网络Network

- libvirt默认会创建一个NAT网桥，用于虚拟机和外界进行沟通。
- 除了NAT，libvirt还支持以下几种网络配置
  - bridge - bridge创建了一个虚拟设备，它通过一个物理接口直接共享数据。使用场景为：宿主机有静态网络、不需与其它域连接、要占用全部进出流量，并且域运行于系统层级。
  - network - 这是一个虚拟网络，它可以与其它虚拟机共用。使用场景为：宿主机有动态网络（例如：NetworkManager）或使用无线网络。
  - macvtap - 直接连接到宿主机的一个物理网络接口。
  - user - 本地网络，仅用于用户会话。

#### 7. 快照Snapshot

虚拟机快照保存了虚拟机在某个指定时间点的状态（包括操作系统和所有的程序），利用快照，我们可以恢复虚拟机到某个以前的状态，比如测试软件的时候经常需要回滚系统

##### 管理快照

```bash
virsh snapshot-create-as domain snapshot1 --ddisk-only --atomic		# 创建快照
virsh snapshot-list domain		# 查看快照
virsh snapshot-dumpxml centos snapshot1		# 查看快照xml文件
```



#### 8. libvirt编程控制

libvirt提供编程语言的SDK，你可以通过编程来控制虚拟机。

```bash
apt install libvirt-python		# 下载所需组件
python3
ython 3.8.10 (default, Jun  2 2021, 10:49:15) 
[GCC 9.4.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import libvirt
>>> con = libvirt.open("qemu:///system")
>>> con
<libvirt.virConnect object at 0x7fb2dcb50040>
>>> dom = con.lookupByName("centos")
>>> dom
<libvirt.virDomain object at 0x7fb2dca8b220>
>>> dom.ID()
4
```

