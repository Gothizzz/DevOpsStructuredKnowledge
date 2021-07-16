# 网络基础

## 1. TCP/IP协议基础知识

### 1. Internet的历史

#### Internet -- "冷战的产物"

1958年美国总统埃森豪威尔向美国国会提出简历DARPA(Defense Advanced Research Project Agency)，即国防部高级研究计划署，简称ARPA。

1968年6月DARPA提出“资源共享计算机网络”（Resource Sharing Computer Networks），目的在于让DARPA的所有电脑互联起来，这个网络就叫ARPAnet，即“阿帕网”，是Internet的最早雏形。

早期的ARPAnet使用网络控制协议（Network Control Protocol, NCP），不能互联不同类型的计算机和不同类型的操作系统，没有纠错功能。

1973年由Kahn和Vinton Cerf两人合作为ARPAnet开发了新的互联网协议。

1974年12月两人正式发表了第一份TCP协议详细说明，但此协议在有数据包丢失时不能有效的纠正。



#### 网络互联促成了TCP/IP协议的产生

TCP协议分成了两个不同的协议：

​	用来检测网络传输中差错的传输控制协议TCP

​	专门负责对不同网络进行互联的互联网协议IP

从此，TCP/IP协议诞生

1983年ARPAnet上停止使用NCP，互联网上的主机全部使用TCP/IP协议。TCP/IP协议成为Internet中的“世界语”。



### 2. 网络的体系结构

网络采用分而治之的方法设计，将网络的功能划分为不同的模块，以分层的形式有机结合在一起。

每层实现不同的功能，其内部实现方法对外部其他层次来说是透明的。每层向上层提供服务，同时使用下层提供的服务。

网络体系结构即指网络的层次结构和每层所使用协议的集合。

两类非常重要的体系结构：OSI与TCP/IP。

#### OSI参考模型及TCP/IP参考模型

![image-20210706124812316](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706124812316.png)

OSI模型相关的协议已经很少使用，但模型本身非常通用。

OSI模型一共有7层，是一个理想化的模型，但是尚未有完整的实现。

TCP/IP协议一共有4层，是Internet事实上的工业标准。



### 3. TCP/IP协议族

#### 常用协议

TCP (Transport Control Protocol)	传输控制协议

IP (Internet Protocol)	网间协议

UDP (User Datagram Protocol)	用户数据报协议

ICMP (Internet Control Message Protocol)	互联网控制信息协议

SMTP (Simple Mail Transfer Protocol)	简单邮件传输协议

SNMP (Simple Network Manage Protocol)	简单网络管理协议

HTTP (Hypertext Transfer Protocol)	超文本传输协议

FTP (File Transfer Protocol)	文件传输协议

ARP (Address Resolution Protocol)	地址解析协议



### 4. TCP和UDP协议

#### 1. TCP协议

是一种面向连接的传输层协议，它能提供高可靠性通信（即数据无误、数据无丢失、数据无失序、数据无重复到达的通信）

![image-20210706130232191](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706130232191.png)

适用情况：

1. 适合于对传输质量要求较高，以及传输大量数据的通信
2. 在需要可靠数据传输的场合，通常使用TCP协议
3. MSN/QQ等即时通讯软件的用户登录账号管理相关的功能通常采用TCP协议

#### 2. TCP三次/四次挥手

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimage.mamicode.com%2Finfo%2F201801%2F20180123121700029891.png&refer=http%3A%2F%2Fimage.mamicode.com&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1628140254&t=29dbe78dda472665ccb81f62709e1baa)

![img](https://gimg2.baidu.com/image_search/src=http%3A%2F%2Fimg-blog.csdnimg.cn%2Fimg_convert%2Fbbdbeab7aac1f904b223f4493a4650e0.png&refer=http%3A%2F%2Fimg-blog.csdnimg.cn&app=2002&size=f9999,10000&q=a80&n=0&g=0n&fmt=jpeg?sec=1628140324&t=12d3d3ad804b9954fa5577821a93f1ea)

#### 3 UDP协议

UDP(User Datagram Protocol) 用户数据报协议，是**不可靠的无连接的协议**。在数据发送前，因为不需要进行连接，所以可以进行高效率的数据传输。



使用情况：

1. 在接收到数据，给应答较困难的网络中使用UDP。（如：无线网络）
2. 适合用于广播和组播通信当中。
3. MSN/QQ/Skype等即时通讯软件的点对点文本通讯以及音视频通讯通常采用UDP协议。
4. 流媒体、VOD、VoIP、IPTV等网络多媒体服务中通常采用UDP方式进行实时数据传输。

同时，一个UDP应用可同时作为应用的客户或服务器。由于UDP协议并不需要建立一个明确的连接，因此建立UDP应用要比建立TCP应用简单的多。



**共同点**：同为传输层协议

**不同点**：

- TCP：有连接，可靠
- UDP：无连接，不可靠

#### 4 协议的选择

##### 1. 对数据可靠性的要求

对数据要求高可靠性的应用需选择TCP协议，如验证、密码字段的传送都是不允许出错的，而对数据的可靠性要求不那么高的应用可选择UDP传送。

##### 2. 应用的实时性

TCP协议在传送过程中要使用三次握手，重传确认等手段来保证数据传输的可靠性。使用TCP协议会有较大的时延，因此不适合对实时性要求较高的应用，如VOIP、视频监控等。相反，UDP协议在这些应用中能发挥很好的作用。

##### 3. 网络的可靠性

由于TCP协议的提出主要是解决网络的可靠性问题，它通过各种机制来减少错误发生的概率。因此，在网络状况不是很好的情况下需选用TCP协议（如在广域网等情况），但是若在网络状况很好的情况下（如局域网等）就不需要再采用TCP协议，而选择UDP协议来减少网络负荷。

## 2. Linux基础网络编程

### 1. Socket

#### 1. Socket的概念

在Linux中的网络编程是通过socket接口来进行的。socket是一种特殊的I/O接口，它也是一种**文件描述符**。它是一种常用的进程之间的通信，而且通过网络能够在不同的机器上的进程之间进行通信。

Socket也有类似于打开文件的函数调用，该函数返回一个整型的socket描述符，随后的连接建立，数据传输等操作都是通过socket来实现的。

#### 2. Socket的类型

##### 1. 流式socket(SOCK_STREAM)

流式套接字提供可靠的、面向连接的通信流；它使用**TCP协议**，从而保证了数据传输的正确性和顺序性。

##### 2. 数据报socket(SOCK_DGRAM)

数据报套接字定义了一种无连接的服务，数据通过相互独立的报文进行传输，是无序的，而且不保证是可靠、无差错的。它使用数据报协议UDP。

##### 3. 原始socket

原始套接字允许对底层协议如IP或ICMP进行直接访问，它功能强大但使用较为不便，主要用于一些协议的开发。



#### 3. Socket的位置

![image-20210706160439749](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706160439749.png)

### 2. 网络地址

#### 1. IP地址

IP地址是Internet中主机的标识

Internet中的主机要与别的机器通信必须应具有一个IP地址

IP地址为32位(IPV4)或者128位(IPV6)

每个数据包都必须携带目的IP地址和源IP地址，路由器依靠此信息为数据包选择路由



表现形式：IP地址是一个32位的二进制数，通常被分割为4个“8位二进制数”（也就是4个字节）。通常点分形式，如202.8.64.10，最后都会转换为一个32位无符号整数。

![image-20210706160951435](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706160951435.png)

#### 2. 网络地址

##### A类地址

第一字节为网络地址，其他3个字节为主机地址。第1字节的最高位固定为0

1.0.0.1 --- 126.255.255.255

##### B类地址

第1字节和第2字节是网络地址，其他2个字节是主机地址。第1字节的前两位固定为10

128.0.0.1 --- 191.255.255.255

##### C类地址

前3个字节是网络地址，最后1个字节是主机地址。第1字节的前3位固定为110

192.0.0.1 --- 223.255.255.255

##### D类地址（组播地址）

不分网络地址和主机地址，第1字节的前4位固定为1110

224.0.0.11 --- 239.255.255.255



#### 3. IP地址的转换函数

inet_ation ()

将strptr所指的字符串转换成32位的网络字节序二进制值。

```c
#include <arpa/inrt.h>
int inet_aton(const char *strptr, struct in_addr *addrptr);
```



inet_addr ()

功能同上，返回转换后的地址。

```C
int_addr_t inet_addr(const char *strptr);
```



inet_ntoa ()

将32位网络字节序二进制地址转换成点分十进制字符串。

```C
char *inet_ntoa(struct in_addr inaddr);
```



### 3. 端口号

为了区分一台主机接收到的数据包应该转交给哪个进程来进行处理，使用端口号来区分

TCP端口号与UDP端口号独立

端口号一般由IANA(Interner Assigned Numbers Authority)管理

​	众所周知端口：1~1023（1-255之间为众所周知端口，256-1023端口通常由UNIX系统占用）

​	注册端口：1024~49150

​	动态或私有端口：49150~65535

#### 套接字和端口

![image-20210706213958475](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706213958475.png)

### 4. 字节序

#### 1. 字节序

不同类型CPU的主机中，内存存储多字节整数序列有两种方法，成为主机字节序（HBO）：

##### 小端序(little-endian)

低序字节存储在低地址，将低字节存储在起始地址。Intel、AMD等采用的是这种方式。

##### 大端序(big-endian)

高序字节存储在低地址，将高字节存储在起始地址。ARM、Motorola等采用这种方式。

![image-20210706214815894](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706214815894.png)



网络中传输的数据必须按**网络字节序**，即大端字节序。

在大部分PC机上，当应用进程将整数送入socket前，需要转化成网络字节序；当应用进程从socket取出整数后，要转化为小端字节序。

#### 2. 网络字节序(NBO - Network Byte Order)

把给定系统所采用的字节序称为主机字节序，为了避免不同类别主机之间在数据交换时由于字节序不同而导致的差错，引入了网络字节序。使用统一的字节顺序，**避免兼容性问题**。

不同主机的HBO(Host Byte Order) 是不一样的，这与CPU的设计有关。

Motorola 68K系列，ARM系列，HBO与NBO是一致的。

Inter X86系列，HBO与NBO是不一致的。



#### 3. 字节序转换函数

这里用到了四个函数：htons (), ntohs (), htonl ()和htohl ()。这四个函数分别实现网络字节序和主机字节序的转化，这里的h代表host，n代表network，s代表short，l代表long。通常16位的IP端口号用s表示，而IP地址用l表示。

![image-20210706220222800](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706220222800.png)

### 5. Socket基础编程

#### 1. 网络编程相关API

**网络编程常用函数：**

##### 1. socket ()

用于建立一个socket连接，可指定socket类型等信息。在建立了socket连接之后，可对sockaddr或sockaddr_in结构进行初始化，**以保存所建立的socket地址信息**。

![image-20210706223134048](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706223134048.png)

![image-20210706223412344](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706223412344.png)

**地址结构的一般用法：**

定义一个struct sockaddr_in类型的变量并清空

```c
struct sockaddr_in myaddr;
memset (&myaddr, 0, sizeof(myaddr));
```

填充地址信息

```c
myaddr.sin_family = AF_INET;
myaddr.sin_port = htons (8888);
myaddr.sin_addr.s_addr = inet_addr ("192.18.1.100");
```

##### 2. bind ()

用于将**本地IP地址绑定到端口号**，若绑定其他IP地址则不能成功。另外，它主要用于TCP连接，而在UDP的连接中则无必要。

![image-20210706224141337](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706224141337.png)

![image-20210706224231342](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706224231342.png)

##### 3. listen ()

在服务端程序成功建立套接字和与地址进行绑定之后，还需要准备在该套接字上接收新的连接请求。此时**调用listen ()函数来创建一个等待队列**，在其中存放未处理的客户端连接请求。

![image-20210706224505321](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706224505321.png)

完成listen（）调用后，socket变成了监听socket（listening socket）

![image-20210706224631551](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706224631551.png)



##### 4. accept ()

服务端程序调用**listen ()函数创建等待队列**之后，调用accept ()函数等待并接收客户端的连接请求。它通常从bind ()所创建的等待队列中取出**第一个未处理**的连接请求。

![image-20210706225128228](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706225128228.png)

listen（）和accept（）是TCP服务端使用的函数。

![image-20210706225417382](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706225417382.png)



##### 5. conect ()

该函数在TCP中是用于bind ()的之后的**客户端**，用于与服务器建立连接，而在UDP中由于没有了bind ()函数，因此用connect ()有点类似bind ()函数的作用。

![image-20210706225710526](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706225710526.png)

connect（）是客户端使用的系统调用。

![image-20210706225816815](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706225816815.png)



##### 6. send ()和recv ()

这两个函数分别用于发送和接收数据，可以用在TCP中，也可以用在UDP中。当用在UDP时，可以在connect ()函数建立连接之后再用。

![image-20210706225908647](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706225908647.png)

##### 7. sendto ()和recvfrom ()

这两个函数的作用与send ()和recv ()类似，也可以用在TCP和UDP中。当用在TCP时，后面的几个与地址有关参数不起作用，函数作用等同于send ()和recv ()；当用在UDP时，可以用在之前没有使用connect ()的情况下，这两个函数可以自动寻找指定地址并进行连接。

![image-20210706230121712](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210706230121712.png)

#### 2. 套接字关闭

关闭双向通信

```c
int close (int sockfd);  
```

TCP连接是双向的（是可读写的），当我们使用close时，会把读写通道都关闭，有时候我们只希望关闭一个方向，这个时候我们可以使用shutdown函数。

```c
int shutdown (int sockfd, int howto);
```

针对不同的howto，系统会采取不同的关闭方式

howto=0，关闭读通道，但是可以继续往套接字写数据。

howto=1，和上面相反，关闭写通道，只能从套接字读取数据。

howto=2，关闭读写通道，和close（）一样。





## 3. 客户端和服务器的通信程序

### 1. TCP协议流程图

![image-20210707132627065](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210707132627065.png)

### 2. UDP服务端/客户端流程

![image-20210707132902807](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210707132902807.png)

![image-20210707132943838](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210707132943838.png)

## 4. 服务端编程示例

### TCP_server.c

```C
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/shm.h>
#include <stdio.h>
#include <unistd.h>

#define QUEUE 20
#define BUFFER_SIZE 1024

int main()
{
    //define socket
    int server_sockfd = socket(AF_INET, SOCK_STREAM, 0);
    
    //define sockaddr_in
    struct sockaddr_in server_sockaddr;
    server_sockaddr.sin_family = AF_INET;
    server_sockaddr.sin_port = htons(8887);
    server_sockaddr.sin_addr.s_addr = inet_addr("192.168.31.229");
    
    //bind,success->0,fail->1
    if(bind(server_sockfd, (struct sockaddr *)&server_sockaddr, sizeof(server_sockaddr)) == -1)
    {
        perror("bind");
        exit(1);
    }
    
    //listen,success->0,fail->1
    if(listen(server_sockfd, QUEUE) == -1)
    {
        perror("listen");
        exit(1);
    }
    
    //client socket
    char buffer[BUFFER_SIZE];
    struct sockaddr_in client_addr;
    socklen_t length = sizeof(client_addr);
    
    int conn = accept(server_sockfd, (struct sockaddr *)&client_addr, &length);
    if(conn < 0 )
    {
        perror("connect");
        exit(1);
    }
    
    while(1)
    {
        memset(buffer, 0, sizeof(buffer));
        int len = recv(conn, buffer, sizeof(buffer), 0);
        if(strcmp(buffer, "exit\n") == 0)
            break;
        fputs(buffer, stdout);
        send(conn, buffer, len, 0);
    }
    
    close(conn);
    close(server_sockfd);
    
    
    return 0;
}
```



### TCP_client.c

```c
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/shm.h>
#include <stdio.h>
#include <unistd.h>

#define QUEUE 20
#define BUFFER_SIZE 1024

int main()
{
    //define socket
    int sock_cli = socket(AF_INET, SOCK_STREAM, 0);
    
    //define sockaddr_in
    struct sockaddr_in servaddr;
    memset(&servaddr, 0, sizeof(servaddr));
    servaddr.sin_family = AF_INET;
    servaddr.sin_port = htons(8887);
    servaddr.sin_addr.s_addr = inet_addr("192.168.31.229");
    
    if(connect(sock_cli, (struct sockaddr *)&servaddr, sizeof(servaddr)) <0)
    {
        perror("connect");
        exit(1);
    }
        
    char sendbuf[BUFFER_SIZE];
    char recvbuf[BUFFER_SIZE];
    
    while(fgets(sendbuf, sizeof(sendbuf), stdin) != NULL)
    {
        send(sock_cli, sendbuf, strlen(sendbuf), 0);//send data
        if(strcmp(sendbuf, "exit\n") == 0)
            break;
        recv(sock_cli, recvbuf, strlen(recvbuf), 0);//recv data
        fputs(recvbuf,stdout);
        
        memset(sendbuf, 0, sizeof(sendbuf));
        memset(recvbuf, 0, sizeof(recvbuf));
        
    }    
    
    close(sock_cli);
    
    return 0;
}
```



### UDP_server.c

```c
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/shm.h>
#include <stdio.h>
#include <unistd.h>

#define RECVLENTH 120
#define SENDLENTH 120

int main(int argc, char **argv)
{
    int sockefd = socket(AF_INET, SOCK_DGRAM, 0);
    if(sockefd == -1)
    {
        perror("socket failed!");
    }
    
    struct sockaddr_in saddr, caddr;
    memset(&saddr, 0, sizeof(struct sockaddr_in));
    saddr.sin_family = AF_INET;
    saddr.sin_port = htons(6666);
    saddr.sin_addr.s_addr = inet_addr("192.168.31.229");
    
    int ret = bind(sockefd, (struct sockaddr*)&saddr, sizeof(struct sockaddr));
    if(ret == -1)
    {
    	perror("bind failed!");
    }
    
    char buf1[SENDLENTH] = {"hello client!"};
    sendto(sockefd, buf1, strlen(buf1), 0, (struct sockaddr*)&caddr, sizeof(struct sockaddr));
    
    char buf[RECVLENTH];
    memset(buf, 0, RECVLENTH);
    int size = sizeof(struct sockaddr);
    recvfrom(sockefd, buf, RECVLENTH, 0, (struct sockaddr*)&caddr, &size);
    printf("[server recv]:%s\n",buf);
  
    close(sockefd);
    
    return 0;
}
```



### UDP_client.c

```c
#include <sys/types.h>
#include <sys/socket.h>
#include <netinet/in.h>
#include <arpa/inet.h>
#include <string.h>
#include <stdlib.h>
#include <fcntl.h>
#include <sys/shm.h>
#include <stdio.h>
#include <unistd.h>

#define RECVLENTH 120
#define SENDLENTH 120

int main(int argc, char **argv)
{
    int sockefd = socket(AF_INET, SOCK_DGRAM, 0);
    if(sockefd == -1)
    {
        perror("socket failed!");
    }
    
    struct sockaddr_in saddr, caddr;
    memset(&saddr, 0, sizeof(struct sockaddr_in));
    saddr.sin_family = AF_INET;
    saddr.sin_port = htons(6666);
    saddr.sin_addr.s_addr = inet_addr("192.168.31.229");
    
    char buf[SENDLENTH] = "hello server!";
    sendto(sockefd, buf, strlen(buf), 0, (struct sockaddr*)&saddr, sizeof(struct sockaddr));
    
    char buf1[RECVLENTH];
    memset(buf1, 0, RECVLENTH);
    int size = sizeof(struct sockaddr);
    recvfrom(sockefd, buf1, RECVLENTH, 0, (struct sockaddr*)&caddr, &size);
    printf("[client recv]:%s\n",buf1);
    
    close(sockefd);
    
    return 0;
}
```



# 基础服务

## 1. DHCP服务配置

动态主机设置协议（Dynamic Host Configuration Protocol），又称动态主机组态协定，是一个用于IP网络的网络协议

DHCP协议位于OSI模型的应用层，使用UDP协议工作

DHCP协议主要有两个用途：

- 用于内部网或网络服务供应商自动分配IP地址给用户
- 用于内部网管理员对所有电脑作中央管理

### 1. DHCP服务原理

- 动态主机设置协议（DHCP）是一种使网络管理员能够集中管理和自动分配IP网络地址的通信协议。在IP网络中，每个连接到Internet的设备都需要分配唯一的IP地址。DHCP使网络管理员能从中心结点监控和分配IP地址。当某台计算机移到网络中的其他位置时，能自动收到新的IP地址。
- DHCP使用了租约的概念，或称为计算机IP地址的有效期。租用时间是不定的，主要取决于用户在某地连接internet需要多久，这对于教育行业和其他用户频繁改变的环境是很实用的。透过较短的租期，DHCP能够在一个计算机比可用IP地址多的环境中动态地重新配置网络。DHCP支持为计算机分配静态地址，如需要永久性IP地址的Web服务器。
- DHCP和另一个网络IP管理协议BOOTP类似。目前两种配置管理协议都得到了普遍使用，其中DHCP更为先进。某些操作系统，如Windows Server，带有DHCP服务器。

### 2. 安装DHCP服务器

```shell
rpm -qa | grep dhcp
yum/dnf install dhcp-server -y
systemctl status dhcpd.service
```

### 3. DHCP服务器配置

```shell
option routers 222.205.197.1;
option subnet-mask 255.255.255.0;
default-lease-time 36000;
max-lease-time 360000;

subnet 204.254.239.0 netmask 255.255.255.224{
	subnet-specific parameters...
	range 204.254.239.10 204.254.239.30;
}

group{
	group-specific parameters...
	host zappo.test.isc.org{
		host-specific parameters...
	}
}
```

/etc/dhcp/dhcpd.conf

```shell
default-lease-time 86400;
max-lease-time 86400;

authoritative;

log-facility local7;

subnet  172.23.254.0 netmask 255.255.255.0 {
	range  172.23.254.100 172.23.254.200;
	
	option domain-name "dhcp.linux.cn";
	option domain-name-servers 192.168.1.50, 8.8.8.8, 8.8.4.4;
	option routers 192.168.1.1;
}
```



## 2. HTTP服务

HTTP服务背后是Web服务器提供的服务。

每一个Web服务器程序都需要从网络接收HTTP请求，然后提供HTTP回复给请求者。HTTP回复一般包含一个HTML文件，有时也可以包含纯文本文件、图像或其他类型的文件。

一般来说这些文件都存储在网页服务器的本地文件系统中，而URL和本地文件名都有一个阶级组织结构的，服务器会简单的把URL对照到本地文件系统中。当正确安装和设置好网页服务器软件，服务器管理员会从服务器软件放置文件的地方指定一个本地路径名为根目录。

常见的Web服务器包括：Apache Httpd、Nginx、IIS、LiteSpeed Web Server

### Apache Httpd

Apache Http Server（简称Apache）是Apache软件基金会的一个开放源码的网页服务器软件，可以在大多数电脑操作系统中运行。由于其跨平台和安全性，被广泛使用，是最流行的Web服务器软件之一。它快速，可靠并且可通过简单的API扩展，将Perl/Python等解释器编译到服务器中。

Apache HTTP通常和脚本语言比如PHP，数据库Mysql一起工作，合称为LAMP栈（Linux、Apache、Mysql、PHP）

根据Netcraft的统计，目前活跃站点市场占有率最高的HTTPD服务器仍是Apache。

#### 1. Apache HTTPd的安装

```shell
rpm -qa | grep http
yum install httpd -y
systemctl start httpd
systemctl status httpd
```

#### 2. Apache HTTPd的配置文件

Apache默认的配置文件为 /etc/httpd/conf/httpd.conf

网站根目录下的.htaccess 也可以配置部分表现

#### 3. 虚拟主机的配置

```shell
<VirtualHost *:80>
	ServerName www.example.com
	ServerAlias example.com
	DocumentRoot /var/www/example.com/log/html
	ErrorLog /var/www/example.com/log/error.log 
	CustomLog /var/www/example.com/log/requests.log combined
</VirtualHost>
```

#### 4. 关闭版本号输出

/etc/httpd/conf/httpd.conf

```shell
ServerSignature	Off
ServerTokens	Prod
```

```shell
ServerTokens	Full(or not specified)
	Server sends(e.g.): Server: Apache/2.4.2 (Unix) PHP/4.2.2 MyMod/1.2
ServerTokens	Prod[uctOnly]
	Server sends(e.g.): Server: Apache
ServerTokens	Major
	Server sends(e.g.): Server: Apache/2
ServerTokens	Minor
	Server sends(e.g.): Server: Apache/2.4
ServerTokens	Min[imal]
	Server sends(e.g.): Server: Apache/2.4.2
ServerTokens	OS
	Server sends(e.g.): Server: Apache/2.4.2(Unix)
```

#### 5. 移除无用的modules

- 使用 httpd -M 可获得模块列表

- 使用 httpd -M|wc -l 可以获得模块总数

- 移除一些无用的模块，可以有效的提升Apache的启动速度

  ```
  /etc/httpd/conf.modules.d
  ```

  - mod_dav：提供WebDav协议，一般用不到
  - autoindex：提供自动的索引服务，一般处于安全考虑，关闭
  - status：展示服务器的状态的服务，一般用不到，可以关闭
  - env：设置环境变量的服务，一般用不到
  - filter：请求过滤服务，一般用不到
  - auth_ 类模块：校验模块，一般用不到


#### 6. 关闭Autoindex

在虚拟主机中配置 Options -Indexs 或 IndexIgnore * 可以禁止自动索引



#### 7. 保护配置文件

使用chattr +i /etc/httpd/conf/httpd.conf 可以保护配置文件被修改

使用chattr -i /etc/httpd/conf/httpd.conf 可以取消保护

#### 8. 关闭Symbol Link跟踪

在虚拟主机中配置Options FollowSymLinks会导致符号连接被跟踪，从而导致信息泄露



## 3. FTP服务

文件传输协议（File Transfer Protocol）是一个用于在计算机网络上在客户端和服务器之间进行文件传输的应用层协议。

FTP服务一般运行在20和21两个端口。端口20用于在客户端和服务器之间传输数据流，而端口21用于传输控制流，并且是命令通向ftp服务器的进口。

当数据通过数据流传输时，控制流处于空闲状态。而当控制流空闲很长时间后，客户端的防火墙会将其会话置为超时，这样当大量数据通过防火墙时，会产生一些问题，此时，虽然文件可以成功的传输，但因为控制会话会被防火墙断开，传输会产生一些错误。

FTP虽然可以被终端用户直接使用，但是它是设计成被FTP客户端程序所控制。

运行FTP服务的许多站点都开放匿名服务，在这种设置下，用户不需要账号就可以登录服务器，默认情况下，匿名用户的用户名是“anonymous”。这个账号不需要密码，虽然通常要求输入用户的邮件地址作为认证密码，但这只是一些细节或者此邮件地址根本不被确定，而是依赖于FTP服务器的配置情况。

### 1. FTP的主动模式和被动模式

FTP有两种模式：主动和被动

主动模式要求客户端和服务器端同时打开并且监听一个端口以创建连接。在这种情况下，客户端由于安装了防火墙会产生一些问题。所以，创立了被动模式。

被动模式只要求服务器端产生一个监听相应端口的进程，这样就可以绕过客户端安装了防火墙的问题。

### 2. VSFTP

VSFTP（Very Secure FTP Daemon）是一个为Unix类系统开发的轻量，稳定和安全的FTP服务器端。

在Linux中，可以使用vsftp来配置一个FTP Server

### 3. vsftpd的安装

```shell
rpm -qa|grep vsftpd
yum install vsftpd -y
systemctl start vsftpd
systemctl status vsftpd
```

### 4. vsftpd的基本配置

vsftpd的配置文件在/etc/vsftpd/vsftpd.conf

关闭匿名登录需要设置 anonymous_enable 为 NO

允许本地用户作为FTP用户需要设置 local_enables 为 YES

允许写入需要设置 write_enable 为 YES

限制用户只能在自己的目录下管理文件需要设置 chroot_local_user 为YES

设置FTP登陆时显示的文字只需要修改 ftpd_banner 的值



## 4. DNS服务

域名解析服务（Domain Name System）是一个Internet服务，相互映射IP地址和完全限定域名（FQDN）。通过这种方式，使用DNS将不再需要记住IP地址。运行DNS的计算机成为名称服务器。

### 1. DNS的记录类型

#### 主机记录（A记录）

RFC 1035定义，A记录是用于名称解析的重要记录，它将特定的主机名映射到对应主机的IP地址上。

#### 别名记录（CNAME记录）

RFC 1035定义，CNAME记录用于将某个别名指向到某个A记录上，这样就不需要再为某个新名字另外创建一条新的A记录。

#### IPv6主机记录（AAAA记录）

RFC 3596定义，与A记录对应，用于将特定的主机名映射到一个主机的IPv6地址。

#### 服务位置记录（SRV）记录

RFC 2782定义，用于定义提供特定服务的服务器的位置，如主机（hostname），端口（port number）等。

#### 域名服务器记录（NS记录）

用来指定该域名由哪个DNS服务器来进行解析。您注册域名时，总有默认的DNS服务器，每个注册的域名都是由一个DNS域名服务器来解析的，DNS服务器NS记录地址一般以以下的形式出现：ns1.domain.com、ns2.domain.com等。简单来说，NS记录是指定由哪个DNS服务器解析你的域名。



### 2. 常用的DNS服务器软件

#### 1. Bind

Bind（Berkeley Internet Name Domain）是域名系统（DNS）协议的一个完整的、高度可移植的实现。

##### 1. Bind的安装

```shell
rpm -qa|grep bind
dnf install bind bind-utils -y
systemctl start named
systemctl status named
```

##### 2. Bind的配置

/etc/named.conf

```shell
zone "linux.cn" IN {
	type master;
	file "linux.cn.zone";
	allow-update {none;};
};
```

/var/named/linux.cn.zone

```shell
$TTL 86400
@	IN	SOA		ns1.linux.cn. root.linux.cn. (
		2013042201	;Serial
		3600		;Refresh
		1800		;Retry
		604800		;Expire
		86400		;Minimum TTL
)
; Specify our two nameservers
		IN	NS	ns1.linux.cn.
		IN	NS	ns2.linux.cn.
; Resolve nameserver hostnames to IP
ns1		IN	A	1.1.1.1
ns2		IN	A	2.2.2.2

; Define hostname -> IP pairs which you wish to resolve
@		IN	A	3.3.3.3
www		IN	A	3.3.3.3
```

#### 2. PowerDNS

#### 3. Dnsmasq



## 5. MySQL服务

MySQL原本是一个开放源码的关系数据库管理系统，原开发者为瑞典的MySQL AB公司，该公司于2008年被昇阳微系统（Sun Microsystems）收购。2009年，甲骨文公司（Oracle）收购昇阳微系统公司，MySQL成为Oracle旗下产品。

MySQL在过去由于性能高、成本低、可靠性好，已经成为最流行的开源数据库，因此被广泛的应用在Internet上的中小型网站中。随着MySQL的不断成熟，它也逐渐用于更大规模网站和应用，比如维基百科、Google和Facebook等网站。非常流行的开源软件组合LAMP中的M指的就是MySQL。

### 1. MySQL数据库特性

- 使用C和C++编写，并使用了多种编译器进行测试，保证源代码的可移植性。
- 支持AIX、BSDi、FreeBSD、HP-UX、Linux、Mac OS、Novell NetWare、NetBSD、OpenBSD、OS/2 Wrap、Solaris、Windows等多种操作系统。
- 为多种编程语言提供了API。这些编程语言包括C、C++、C#、VB.NET、Delphi、Eiffel、Java、PHP、Perl、Python、Ruby和Tcl等。
- 支持多线程，充分利用CPU资源，支持多用户。
- 优化的SQL查询算法，有效的提高查询速度。
- 既能够作为一个单位的应用程序在客户端服务器网络中运行，也能够作为一个程序库而嵌入到其他的软件中。
- 提供多语言支持、常见的编码如中午的GB 2312、BIG5，日文的Shift JIS等都可以用作数据表名和数据列名。
- 提供TCP/IP、ODBC和JDBC等多种数据库连接途径。
- 提供用于管理、检查、优化数据库操作的管理工具。
- 可以处理拥有上千万条记录的大型数据库。



### 2. 安装MySQL服务器

```shell
rpm -qa|grep mysql
dnf install mysql-server -y
systemctl start mysqld
mysql_secure_installation
```

配置文件路径

my.cnf.d





## 6. PostgreSQL服务

PostgreSQL是一个功能强大的开源对象关系数据库管理系统（ORDBMS）。用于安全地存储数据；支持最佳做法，并允许在处理请求时检索它们。

PostgreSQL（也称为Post-gress-Q-L）由PostgreSQL全球开发集团（全球志愿者团队）开发。它不受任何公司或其他私人实体控制。它是开源的，其源代码是免费提供的。

PostgreSQL是跨平台的，可以在许多操作系统上运行，如Linux，FreeBSD，OS X，Solaris和Microsoft Window等。

### 1. PostgreSQL特点

PostgreSQL可在所有主要操作系统（即Linux，Unix（AIX，BSD，HP-UX，SGI IRIX，Mac OS X，Solaris，Tru64）和Windows等）上运行。

PostgreSQL支持文本，图像，声音和视频，并包括用于C/C++，Java，Perl，Python，Ruby，Tcl和开放数据库连接（ODBC）的编程接口。

PostgreSQL支持SQL的许多功能，例如复杂SQL查询，SQL子选择，外键，触发器，视图，事务，多进程并发控制（MVCC），流式复制（9.0），热备。

在PostgreSQL中，表可以设置为从“父”表继承其特征。

可以安装多个扩展以向PostgreSQL添加附加功能。

### 2. 安装PostgreSQL服务器

```shell
rpm -qa|grep postgresql
dnf install postgresql-server -y
postgresql-setup --initdb
systemctl start postgresql
```

### 3. 访问PostgreSQL Cli

```shell
sudo -i -u postgres psql
```

### 4. 创建PostgreSQL用户

```shell
sudo -u postgres createuser --interactive
```

### 5. 创建PostgreSQL数据库

```shell
sudo -u postgres createdb example_db
```





## 7. Redis服务

REmote DIctionary Server是一个由Salvatore Sanfilippo写的 key-value 存储系统，是跨平台的非关系型数据库。

Redis是一个开源的使用ANSI C语言编写、遵守BSD协议、支持网络、可基于内存、分布式、可选持久性的键值对（Key-Value）存储数据库，并提供多种语言的API。

Redis通常被称为数据结构服务器，因为值（Value）可以是字符串（String）、哈希（Hash）、列表（List）、集合（Sets）和有序集合（Sorted sets）等类型。

### 1. Redis特点

- Redis支持数据的持久化，可以将内存中的数据保存在磁盘中，重启的时候可以再次加载进行使用。
- Redis不仅仅支持简单的Key-value类型的数据，同时还提供list、set、zset、hash等数据结构的存储。
- Redis支持数据的备份，即master-slave模式的数据备份。

### 2. Redis优势

- 性能极高：Redis能读的速度是110000次/s，写的速度是81000次/s。
- 丰富的数据类型：Redis支持二进制案例的 Strings、Lists、Hashes、Sets及 Ordered Sets 数据类型操作。
- 原子：Redis的所有操作都是原子性的，意思就是要么成功执行要么失败完全不执行。单个操作是原子性的。多个操作也支持事务，即原子性，通过MULTI和EXEC指令抱起来。
- 丰富的特性：Redis还支持 publish/ subscribe，通知，key过期等特性。

### 3. Redis和其他Key Value的服务想比

- Redis有着更为复杂的数据结构并且提供对他们的原子性操作，这是一个不同于其他数据库的进化路径。Redis的数据类型都是基于基本数据结构的同时对程序员透明，无需进行额外的抽象。
- Redis运行在内存中但是可以持久化到磁盘，所以在对不同数据集进行告诉读写时需要权衡内存，因为数据量不能大于硬件内存。在内存数据库方面的另一个优点是，想比在磁盘上相同的复杂的数据结构，在内存中操作起来非常简单，这样Redis可以做很多内部复杂性很强的事情。同时，在磁盘格式方面他们是紧凑的以追加的方式产生的，因为他们并不需要进行随机访问。

### 4. 安装Redis服务器

```shell
rpm -qa|grep redis
dnf install redis -y
systemctl start redis
redis-cli ping
```



# 自动化运维

## 1. Shell脚本进阶

### 1. Shell脚本规范

#### 1. 脚本的命名与权限

##### 脚本后缀

xxxx.sh

##### 脚本名称

可读性命名方法

start.sh	stop.sh	chk_xxx.sh

##### 执行权限

一定要加执行权限

```shell
chmod +x xxx.sh
```

#### 2. 脚本的基本结构

##### #! shebang

#!/bin/bash

#!/usr/bin/env	bash

##### 注释清晰可读

1. 对脚本的功能进行说明
2. 脚本的参数或帮助函数
3. 脚本的作者和更新记录
4. 函数或复杂命令的说明

##### 功能函数与主函数

your_function() {}

main() {}

```shell
#!/usr/bin/env	bash
#usage: print out Hello World
#author: xxx
#update: 20210607 create
#		 20210710 edit function show
#show the message
show() {
	echo "Hello World"
}
main() {
	show
}
main
```



 ```shell
 #!/usr/bin/env	bash
 #usage: Show code standard of bash script
 #author: xxx
 #update 20210710 create
 
 print_usage() {
 cat <<	EOF
 usage: ${0##=/} {-hv} {-f OUTFILE} {FILE}...
 Show code standard of bash script
 -h			display this help and exit.
 -f OUTFILE	write the result to OUTFILE instead of standard output.
 -v			verbose mode.
 EOF
 }
 
 show() {
 	echo "script parameter is: $@"
 }
 
 main() {
 	show $@
 }
 
 if [ $# -eq 0 ]; then
 	print_usage
 else 
 	main $@
 fi
 ```



#### 3. 变量和函数的命名与引用

##### 1. 变量和函数的命名

- 驼峰或下划线命名法
- 避免使用bash关键字

##### 2. 常量的命名

- 大写字母可用下划线分隔
- 统一在非注释开头声明

##### 3. 变量的使用

- 通过 **${变量名}** 引用

##### 4. 函数的使用

- 所有函数放在常量定义之后
- 函数之间不要夹杂其他代码
- main函数放在脚本最后调用



#### 4. 脚本中的文件路径

1. 相对路径和绝对路径
2. 建议使用绝对路径
   - 相对路径依赖脚本执行时的目录
   - 能够规避一些可能出现的异常问题

3. 如何获取脚本所在目录

```shell
$(cd $(dirname $0) && pwd)
$(dirname $(readlink -f $0 ))
```

#### 5. 日志输出规范

##### 为什么需要

需要记录执行过程

##### 单独封装函数

log() {}

##### 日志格式

可参考log4j，包含日期时间，日志级别，日志信息

##### 输出

重定向到文件



### 2. Shell公共库函数

#### 1. 了解系统公共函数库

##### 1. Linux系统的shell脚本

- /etc/init.d/network
- /etc/init.d/sshd
- /etc/init.d/ftpd

##### 2. 以CentOS 7.x为例

- /etc/init.d/function

**checkpid 函数**，根据进程号检查进程是否存在

```shell
#check if any of $pid (could be plural) are running
checkpid() {
	local i
	
	for i in $* ; do
		[ -d "/proc/$i" ] && return 0
	done
	return 1
}
```

**action 函数**，打印信息并执行指定命令，根据命令执行结果调用 success 或者 failure 函数

```shell
# Run some action. Log its output.
action() {
	lcoal STRING rc
	
	STRING=$1
	echo -n "$STRING "
	shift
	"$@" && success $"$STRING" || failure $"$STRING"
	rc=$?
	echo
	return $rc
}
```



#### 2. 如何使用公共函数库

1. 调用系统公共函数库中的函数

在脚本的非注释行前执行 . /etc/init.d/functions 或 source /etc/init.d/functions

2. 自建一个公共函数库

```shell
#!/bin/bash

. /etc/init.d/functions

my_function() {
	if [ "$1" == "Linux" ]; then
		return 0
	else
		return 1
	fi
}

action "Checking system Linux" my_function "Linux"
action "Checking system Windows" my_function "Windows"
```



### 3. Shell脚本数组与字符串处理

#### 1. 复杂数组的处理

##### 一维数组

- 数组定义、元素引用、数组长度、数组分片

```shell
#!/bin/bash

# declare the array
declare -a my_array

# define array value
my_array=("aaa" "bbb" "ccc" "ddd")
my_array[0]="eee"

# get array element
echo ${my_array[0]}
echo

# get array all elements
echo ${my_array[*]}
echo ${my_array[@]}
echo

# get number of array elements
echo ${#my_array[*]}
echo ${#my_array[@]}
echo

# get part of array
echo ${my_array[@]:0:3}
echo
```



##### 二维数组

- Shell只有一维数组的概念
- 如何实现二维数组的需求

```shell
#!/bin/bash

my_array=(
	"a1" "a2" "a3"
	"b1" "b2" "b3"
)

len_ele_line=3
len_ele_sum=${#my_array[@]}

for((i=0; i<len_ele_sum; i+=len_ele_line)); do
	echo "==================="
	echo ${my_array[i]}
	echo ${my_array[i+1]}
	echo ${my_array[i+2]}
done
echo "==================="
```



##### 关联数组

- 字典的概念
- 关联数组的定义与元素的访问
- 遍历元素的key和value

```shell
#!/bin/bash

declare -A color
color["read"]="#ff0000"
color["blue"]="#0000ff"
color["black"]="#000000"

for key in ${!color[@]}
do
	echo "${key} -> ${color[${key}]}"
done
```



#### 2. 复杂字符串的处理

##### 1. 字符串的定义

- str=/path/to/file
- str='/path/to/file'
- str="path/to/file"

##### 2. 字符串操作

![image-20210710212003159](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210710212003159.png)



### 4. Shell脚本复杂参数处理

#### 1. 参数的几种常见形式

例：有一个shell脚本，用于处理一个文件中特定日期的数据，并将结果输出到另一个文件中。我们需要有三个参数：输入文件路径、待处理数据的日期、输出文件路径。

##### 1. 参数个数明确、顺序固定

```shell
./handle_data.sh para1 para2 para3
```

参数特点：

1. 参数不能调整位置
2. 参数使用不灵活

```shell
#!/bin/bash
# comments

show_usage() {
	echo "usage: $(basename $0) [inputfile] [date] [outputfile]"
}

chk_inputpath() {
	echo "param of path: $1"
}

chk_date() {
	echo "param of date: $1"
}

chk_outputpath() {
	echo "param of path: $1"
}

main() {
	chk_inputpath $1
	chk_date $2
	chk_outputpath $1
}

if [ $# -eq 3 ]; then
	main $@
else
	show_usage
fi
```



##### 2. 若有缺省参数，通过命令行选项传参（空格分隔）

```shell
./handle_data.sh -input para1 -date para2 -output para3
```

参数特点：

1. 参数可以缺省
2. 参数顺序可以不固定
3. 命令行选项与参数值通过空格分隔

```shell
#!/bin/bash
# comments

while [ $# -gt 0 ]
do
	key="$1"
	case $key in
		-input)
			INPUT="$2"
			echo "param of input: ${INPUT}"
			shift
			shift;;
		-date)
			DATE="$2"
			echo "param of date: ${DATE}"
			shift
			shift;;
		-output)
			OUTPUT="$2"
			echo "param of output: ${OUTPUT}"
			shift
			shift;;
		*)
			echo "param seems error!"
			echo "usage: $(basename $0) [options]"
			exit 1
			;;
	esac
done		
```



##### 3. 若有缺省参数，通过命令行选项传参（等号分隔）

```shell
./handle_data.sh -input=para1 -date=para2 -output=para3
```

参数特点：

1. 参数可以缺省
2. 参数顺序可以不固定
3. 命令行选项与参数值通过等号分隔

```shell
#!/bin/bash
# comments

for i in "$@"
do
	case $1 in
		-input=*)
			INPUT="${i#*=}"
			echo "param of input: ${INPUT}"
			;;
		-date=*)
			DATE="${i#*=}"
			echo "param of date: ${DATE}"
			;;
		-output=*)
			OUTPUT="${i#*=}"
			echo "param of output: ${OUTPUT}"
			;;
		*)
			echo "paramter seems error!"
			echo "Usage: `basename $0` [options]"
			exit 1
			;;
	esac
done
```



#### 2. getopts 命令介绍

```shell
getopts [option[:]] [DESCRIPTION] VARIABLE
```

内置命令，一般用在循环中。每次循环都会检查下一个命令选项。

两个内置变量

OPTARG：用于保存每个选项后面的参数

OPTIND：表示下一个选项或参数的索引

缺点：不支持长参数（如--debug）

```shell
#!/bin/bash
# comments

while getopts "i:d:o:" opt
do
	case $opt in
	i)
		INPUT=$OPTARG
		echo "param of input: ${INPUT}"
		;;
	d)
		DATE=$OPTARG
		echo "param of date: ${DATE}"
		;;
	o)
		OUTPUT=$OPTARG
		echo "param of output: ${OUTPUT}"
		;;
	?)
		echo "parameter seems error!"
		echo "Usage: `basename $0` [options]"
		exit 1
		;;
	esac
done
```



### 5. Shell脚本的信号捕获

#### 1. Linux进程信号

常见的进程信号（kill -l）

![image-20210711015917635](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210711015917635.png)



#### 2. 信号捕获的使用场景

##### 我们希望shell脚本在运行时不被中断

例如：有一个放在前台执行的shell脚本，不希望被用户的 Ctrl + C 而中止，也就是需要忽略 SIGINT 的系统信号。

##### 我们希望shell脚本被中断后执行待定命令。

例如：有一个数据处理的shell脚本，在被强制结束时，需要做一些临时文件清理的工作。那么当捕捉到 SIGINT 或 SIGTERM 之类的退出信号时，需要再执行一些命令。



#### 3. trap命令使用

##### 捕获信号

```shell
trap "commands" signal-list
```

##### 忽视信号

```shell
trap " " signal-list
```

##### 恢复信号的默认操作

```shell
trap signal-list
```



```shell
#!/bin/bash

trap "echo Goodbye..." EXIT
trap " " INT

for i in $(seq 1 10) ; do
	echo $i
	sleep 1
	if [ $i -eq 7 ];then
		trap INT
	fi
done
```



### 6. Shell脚本单实例运行

#### 1. 单实例运行

##### 背景

计划任务定时执行的shell脚本，当脚本的运行时间可能会超过计划任务的时间间隔时，系统中就会出现多个shell脚本的运行实例。

##### 场景

尤其是当脚本涉及到文件读写、数据库操作等任务时需要注意这种情况。

##### 单实例

使得shell脚本运行的实例个数不超过一个，确保脚本中命令执行的安全性。

##### 思路

shell脚本执行时，先检测当前脚本是否已有实例正在运行，若有则退出。



#### 2. 使用锁文件实现

错误示范：通过查询进程名来判断

正确示范：通过锁文件来判断

1. 若锁文件存在且文件中的进程在运行，退出
2. 将当前程序进程号写入锁文件
3. 开始执行脚本的主体功能
4. 结束时删除锁文件，并用 trap 命令保证

缺点：

1. Linux系统中的进程 pid 号可能会被复用
2. 可能会存在极小概率的异常情况

```shell
#!/bin/bash
# comment

LOCKFILE="test.lock"

if [ -e ${LOCKFILE} ] && kill -0 $(cat ${LOCKFILE}); then
	echo "$0 already running"
	exit
fi

trap "rm -f ${LOCKFILE}; exit" INT TERM EXIT

echo $$ > ${LOCKFILE}

main() {
	sleep 20
}
main

rm -f ${LOCKFILE}
```



#### 3. 使用flock实现

Linux操作系统的文件锁机制

相关命令：flock

```shell
flock [-sxun] [-w #] fd#
flock [-sxon] [-w #] file [-c] command...
```

-s,	--shared：获取一个共享锁，或者称为读锁
**-x,	--exclusive：获取一个排它锁，或者称为写锁，为默认项**

-u,	--unlock：删除一个锁，通常是不需要的，因为在文件关闭时锁会自动删除

**-n,	--nonblock：非阻塞模式，当获取锁失败时，直接返回1而不是继续等待**

-w,	--timeout seconds：设置阻塞超时，没有立即获得锁，等待设置的秒数

```shell
#!/bin/bash
# comment

LOCKFILE="test.lock"
exec 9> ${LOCKFILE}
flock -n 9

if [ "$?" != 0 ]; then
	echo "$0 already running"
	exit 1
fi

main() {
	sleep 20
}

main
```



### 7. Shell脚本常见问题

#### 1. 特殊字符问题

1. 不同操作系统脚本传输
2. 从富文本复制代码

问题：在Windows系统上编辑的shell脚本，拷贝到Linux系统中，发现在每行的末尾会出现 ^M 字符。

解决：使用dos2unix 或 sed 直接替换



问题：脚本中存在一些不可打印的特殊字符，执行时会出现报错。

解决：使用 cat -A 直接查看并删除特殊字符或 od 查看特殊字符的十六进制后 sed 替换

#### 2. 环境变量问题

Shell脚本在console中运行正常，通过计划任务的方式运行会出现异常。

通常，这种问题是环境变量导致的。crontab不会缺省的从用户profile文件中读取环境变量参数。



解决：

1. 脚本中的命令（如java）使用绝对路径，这样就不需要依赖于环境变量
2. 在脚本的开头先加载环境变量

- /etc/profile
- ~/.bash_profile

#### 3. 如何排查问题

##### 代码走读

确定代码逻辑，检查语法错误，考虑异常处理

##### 语法检测

```bash
bash -n script.sh
```

##### 跟踪运行

```bash
bash -x script.sh
```



### 8. Shell复杂脚本实战

#### 1. 脚本目标

假设现在有一个java开发的服务端应用需要编写一个shell脚本实现以下功能

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210711042721875.png" alt="image-20210711042721875" style="zoom:80%;" />

#### 2. 预设脚本参数

```bash
./app.sh start		# 启动应用
./app.sh stop		# 停止应用
./app.sh restart	# 重启应用
./app.sh status		# 查看应用状态
./app.sh log		# 查看操作日志
```

#### 3. 具体实现

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210711043001480.png" alt="image-20210711043001480" style="zoom:80%;" />

```shell
#!/bin/bash
# comments ...
# usage:
# author:
# update:

JAVA=""
APP=""
PID_FILE=""
LOG_FILE=""

show_usage() {
	echo "sh $0 [start|stop|restart|status|log]"
}

log() {
}

app_start() {
}

app_stop() {
}

app_restart() {
}

app_status() {
}

app_log() {
}

main() {
	case "$1" in'
	"start")
		app_start
		;;
	"stop")
		app_stop
		;;
	"restart")
		app_restart
		;;
	"status")
		app_status
		;;
	"log")
		app_log
		;;
	*)
		echo "Parameter Error. Please check!"
		show_usage
		;;
	esac
}

if [ $# -eq 1 ]; then
	main $@
else
	show_usage
fi
```



## 2. Python脚本入门

### 1. Python脚本入门

Python是一种解释型，通用的高级编程语言。

支持面向对象、结构化、函数式编程语言。

开源，社区驱动，现由Python软件基金会管理。

简单易用，功能强大。

跟C语言紧密集成，模块可以转化成C语言以提高性能。

### 2. Python脚本的输入输出

#### 1. 知识补充

##### sys模块简介

sys模块是Python标准库内置的，它提供了一些变量和函数，被解释器所使用。

Python脚本执行时可以传入参数。

代码里获取参数需要通过 sys 模块实现。

##### open函数简介

open(file, mode='r', ...) 函数打开 file 并返回对应的文件对象。

默认返回读取的文本内容。

可指定mode用来写入文件而作为输出。

#### 2. 用户输入和脚本文件参数

##### input获取输入

函数定义：input([prompt])

prompt 为可选参数，如果指定了prompt，则Python运行时将它输出到标准输出，比如终端shell，然后程序暂停等待用户的键盘输入，按下回车后继续执行，所有录入的内容被读取为字符串。

要读取为数字，则需要调用转换函数。

有时候需要将输入作为数字。

请使用转换函数进行转换：

- int()
- float()

大多数时候，我们直接使用编写好的脚本文件。

希望在运行脚本文件的时候，可以传入参数。

此时，需要在代码里用到 sys.argv

sys.argv 是一个列表，第一个参数是脚本的名称。

```python
#!/usr/bin/python3

import sys

print('Number of argument:', len(sys.argv))
print('Argument list:', str(sys.argv))
```

 

#### 3. 输出类型和格式化输出内容

##### 更易读的输出

输出内容一般提供给人们阅读使用。

Python提供了格式化输出选项。

print 函数定义：

```python
print(*object, sep=' ', end='\n', file=sys.stdout, flush=False)
```

使用格式化字符串来输出更易读的内容。









# 系统安全

## 1. iptables安全

### 1. iptables的使用概念

在Linux中内核中，Netfilter子系统负责对网络包进行处理和分发；

iptables便是该子系统的管理控制命令；

iptables将网络包按照处理规则分配给不同的表格，每个表格有对应的处理链；

处理规则由匹配规则和处理目标组成。

#### 1. iptables下的概念

根据Linux内核，iptables中定义了五个不同的挂载点（Hook Ponit），分别是

PreRouting、Input、Forward、PostRouting、Output

#### 2. 挂载点的工作时机

- **Forward**

仅作用于包通过网关计算机，从一个网络接口进入，从另外一个网络接口离开

- **Input**

表示将会把包传递给本地进程

- **Output**

表示包从本地进程生成

- **PostRouting**

表示包离开网络接口

- **PreRouting**

表示包从网络接口进入，进入该挂载点的包已经进行了包的检查和验证

#### 3. tables

iptables内置了三种不同的表来完成工作，分别是NAT、FILTER、MANGLE。

每一个表都配置了不同的处理规则，用于处理网络包的流动。

NAT用于重定向网络地址转换的链接，通常会基于源地址或目标地址。

FILTER用于设置允许进入计算机的包的规则，除非特别设定，默认会使用该表规则进行过滤。

 MANGLE用于进行特殊的包的处理。

#### 4. chain（链）

默认情况下，iptables会包含一些或所有挂载点的链，这些链最初是空的；

你可以通过自定义链的规则，来决定包最终的去向；

你也可以根据自己的需要，自定义链。

#### 5. rule（规则）

iptables由一个或多个匹配以及几个目标组成，这些匹配决定了这个规则会应用在哪些包上，目标则决定了包会被如何处理；

规则的匹配部分和目标部分是可选的，如果没有匹配条件，则任务所有的包都会匹配；如果没有目标，则不对包进行任何处理。

#### 6. match（匹配）

iptables中存在多种匹配；

一些特殊的匹配会需要系统内核的支持；

除了通用的匹配还可以使用 iptables -m 来加载特殊的匹配模块。

#### 7. target（目标）

target定义了与目标规则匹配的情况下，如何对数据包进行操作，iptables内置了四个目标，分别是：ACCEPT、DROP、QUEUE、RETURN；

ACCEPT：允许包通过本阶段，进入下一阶段；停止对本链进行遍历；

DROP：完全停止包处理进程；不再对此包应用任何规则；

QUEUE：将包发送至用户空间；

RETURN：停止调用当前链中的后续规则，并返回到调用链中继续处理。



### 2. iptables命令

#### 1. iptables参数

- 规则操作

-A 追加规则-->iptables -A INPUT

-D 删除规则-->iptables -D INPUT 1(编号)

-R 修改规则-->iptables -R INPUT 1 -s 192.168.12.0 -j DROP 取代现行规则，顺序不变(1是位置)

-I 插入规则-->iptables -I INPUT 1 --dport 80 -j ACCEPT 插入一条规则，原本位置上的规则将会往后移动一个顺位

-L 查看规则-->iptables -L INPUT 列出规则链中的所有规则

-N 新的规则-->iptables -N allowed 定义新的规则

- 通用参数

-p 协议 例：iptables -A INPUT -p tcp

-s 源地址 例：iptables -A INPUT -s 192.168.1.1

-d 目的地址 例：iptables -A INPUT -d 192.168.12.1

-sport 源端口 例:iptables -A INPUT -p tcp --sport 22

-dport 目的端口 例:iptables -A INPUT -p tcp --dport 22

-i 指定入口网卡 例:iptables -A INPUT -i eth0

-o 指定出口网卡 例:iptables -A FORWARD -o eth0

- 动作

DROP 丢弃

ACCEPT 接收

REJECT 拒绝

#### 2. iptables常用命令

iptalbes -L：列举所有命令

iptables -t nat -L：查看NAT表中的所有命令

iptables -F：清空所有规则

iptables -Z：清空所有计数器

iptables -A INPUT -i eth1 -p tcp -m tcp --dport 22 -j DROP：添加一条命令

#### 3. iptables设定默认规则

iptables -P INPUT DROP	# 配置默认的不让进

iptables -P FORWARD DROP	# 默认的不允许转发

iptables -P OUTPUT ACCEPT	# 默认的可以出去

#### 4. iptables -save

iptables -save 可以展示当前的所有表和规则；

其格式可以用于导出 iptables 的规则，后续使用 iptables -restore 进行恢复

#### 5. iptables -restore

iptables -restore 可以读取 iptables -save 保存的规则，并将这些规则添加到当前的 iptables 配置中



### 3. iptables与系统安全

#### 1. ICMP防御

黑客可以通过僵尸网络，针对 ICMP 协议发动 DDoS 攻击，从而使你的业务无法正常服务；

ICMP 的一些漏洞可能会导致你的系统出现安全管理风险；

不是所有的 ICMP 协议的规则都需要阻断，否则会影响使用。

#### 2. ICMP防御规则

```bash
iptables -A INPUT -m conntrack -p icmp --icmp-type 3 --ctstate NEW,ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -m conntrack -p icmp --icmp-type 11 --ctstate NEW,ESTABLISHED,RELATED -j ACCEPT
iptables -A INPUT -m conntrack -p icmp --icmp-type 12 --ctstate NEW,ESTABLISHED,RELATED -j ACCEPT
```

#### 3. 规则说明

- -m conntrack 表示使用了 conntrack 模块来允许处于特定状态的包；在这个规则中，允许那些已经链接链接的包（ESTABLISHED、RELATED），也允许新的数据包；

- -p	配置 ICMP协议；

- --icmp-type	允许那些特定类型的 ICMP 信息

#### 4. ICMP类型

- type3：用于获取目标是否可到达信息；
- type11：用于获取到达目标前，数据包已经超过了 TTL 的生存周期的信息；
- type12：用于获取数据包有错误的 IP 头等信息；
- type0 和 type8：用于返回给源主机主机活动状态的信息，建议在解决网络问题时临时开放；
- type5：重定向消息，可能被黑客利用。

#### 5. 阻止所有未经运行的包

在设定了安全规则后，就可以屏蔽掉所有未经允许的包，从而将规则从黑名单模式调整为更加安全的白名单模式。

```bash
iptables -P INPUT DROP
```



## 2. 系统安全及业务安全

### 1. 用户系统安全

#### 1. 使用root用户运维的危害

使用root用户来进行你的日常运维管理操作，存在极大的安全风险

- 使用root用户更容易在意外执行有高风险命令时产生不可挽回的操作；
- 需要对root用户的账号信息进行分发，容易出现信息安全泄露的问题；

#### 2. sudo命令

sudo是一个以root用户（或其他用户）来控制运行命令访问的程序。它可以配置为允许一个用户像root用户一样来运行所有的命令，或者仅仅一些命令。你也可以配置为无需密码即可使用 sudo 运行命令。

#### 3. 使用sudo的好处

1. 只在执行必要命令的时候使用 root 权限，日常运维使用其它权限，减少出现意外破坏情况的概率；
2. 获取 root 权限时，用户需要输入自己的密码来进行安全校验，而不是输入 root 用户的密码来进行校验；
3. sudo命令可以按照用户进行安全审计，避免都使用 root 用户时审计不便的问题；
4. 关闭了 root 登陆并配置 sudo 的情况下，可以减少黑客针对 root 用户进行定向爆破成功的可能性。

#### 4. 配置sudo权限

编辑 /etc/sudoers 文件，可以编辑具体的 sudo 用户权限

使用 vim /etc/sudoers 或 visudo 命令

```shell
# Members of the admin group may gain root privileges
%admin ALL=(ALL) ALL

# Allow members of group sudo to execute any command
%sudo  ALL=(ALL:ALL) ALL
```

#### 5. 配置sudo用户只能执行特定的命令

```shell
bestony	ALL=(ALL) ALL								# 用户可以执行所有命令
bestony	ALL=(ALL) /usr/bin/systemctl status sshd	# 用户只能执行一个命令
bestony	ALL=(ALL) /usr/bin/systemctl * sshd			# 用户可以执行一组命令
bestony ALL=(ALL) /usr/bin/systemctl status sshd, /usr/bin/systemctl restart sshd			# 用户可以执行多个命令
bestony	ALL=(admin) /usr/bin/echo_help				# 用户只能以特定用户执行命令 sudo -u admin /usr/bin/echo_help
```

#### 6. 一些常用命令

##### 查看当前用户 sudo 权限

```bash
[root@iZuf661irhf5hrgrzovlbyZ ~]# sudo -l
Matching Defaults entries for root on iZuf661irhf5hrgrzovlbyZ:
    !visiblepw, always_set_home, match_group_by_gid, always_query_group_plugin, env_reset, env_keep="COLORS DISPLAY HOSTNAME HISTSIZE KDEDIR LS_COLORS",
    env_keep+="MAIL PS1 PS2 QTDIR USERNAME LANG LC_ADDRESS LC_CTYPE", env_keep+="LC_COLLATE LC_IDENTIFICATION LC_MEASUREMENT LC_MESSAGES", env_keep+="LC_MONETARY
    LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE", env_keep+="LC_TIME LC_ALL LANGUAGE LINGUAS _XKB_CHARSET XAUTHORITY", secure_path=/sbin\:/bin\:/usr/sbin\:/usr/bin

User root may run the following commands on iZuf661irhf5hrgrzovlbyZ:
    (ALL) ALL
```

##### 配置密码有效期

可以使用 chage -l root 查看密码有效期

```bash
[root@iZuf661irhf5hrgrzovlbyZ ~]# sudo -l
Matching Defaults entries for root on iZuf661irhf5hrgrzovlbyZ:
    !visiblepw, always_set_home, match_group_by_gid, always_query_group_plugin, env_reset, env_keep="COLORS DISPLAY HOSTNAME HISTSIZE KDEDIR LS_COLORS",
    env_keep+="MAIL PS1 PS2 QTDIR USERNAME LANG LC_ADDRESS LC_CTYPE", env_keep+="LC_COLLATE LC_IDENTIFICATION LC_MEASUREMENT LC_MESSAGES", env_keep+="LC_MONETARY
    LC_NAME LC_NUMERIC LC_PAPER LC_TELEPHONE", env_keep+="LC_TIME LC_ALL LANGUAGE LINGUAS _XKB_CHARSET XAUTHORITY", secure_path=/sbin\:/bin\:/usr/sbin\:/usr/bin

User root may run the following commands on iZuf661irhf5hrgrzovlbyZ:
    (ALL) ALL
```

可以编辑 /etc/login.defs 设置密码过期时间

```bash
#       PASS_MAX_DAYS   Maximum number of days a password may be used.
#       PASS_MIN_DAYS   Minimum number of days allowed between password changes.
#       PASS_MIN_LEN    Minimum acceptable password length.
#       PASS_WARN_AGE   Number of days warning given before a password expires.
PASS_MAX_DAYS   99999
PASS_MIN_DAYS   0
PASS_MIN_LEN    5
PASS_WARN_AGE   7 # 过期前多少天进行提醒
```

##### 设置安全提醒信息

/etc/motd 文件中存储的信息将会在每一次登陆后展示，从而可以确保在登陆到服务器后，即可看到相关内容。

```bash
[root@iZuf661irhf5hrgrzovlbyZ ~]# cat /etc/motd 

Welcome to Alibaba Cloud Elastic Compute Service !
```

/etc/issue 文件中存储的信息将会在每一次登陆前展示，你可以将信息设定在其中，从而确保可以让用户登陆时看到



### 2. SSH安全

#### 1. 关闭SSH protocol 1

SSH Protocol是SSH协议的第一版，相比于已经在使用的第二版来说，已经不再安全，因此，需要关闭服务器的 SSH Protocol 1

在 /etc/ssh/ssh_config 中查找 Protocol 1,2，移除其中的1即可关闭SSH Protocol

CentOS系从CentOS 7.4 开始，便移除了该选项

#### 2. 关闭root用户登陆

在 /etc/ssh/sshd_config 中查找 PermitRootLogin，并设置为no，即可禁止 root 用户登陆。

#### 3. 关闭用户名密码登陆

在 /etc/ssh/sshd_config 中查找 PasswordAuthentication，并设置为no，即可禁止使用密码登陆。

#### 4. 设置SSH日志输出

在 /etc/ssh/sshd_config 中查找 LogLevel，取消注释，并配置日志等级

#### 5. 设置SSH的端口为非22端口

在 /etc/ssh/sshd_config 中查找port，取消注释，并修改端口为目标端口即可

#### 6. 创建一个SSH登陆Banner

创建 /etc/ssh/sshd-banner，并填入想要显示的内容

在 /etc/ssh/sshd_config 中查找 Banner，取消注释，并其值为 /etc/ssh/sshd-banner 即可



### 3. 安全检查

#### 1. ClamAV

ClamAV杀毒是Linux平台最受欢迎的杀毒软件

支持多种平台，如Linux/Unix、Mac OS X、Windows、OpenVMS

ClamAV是基于病毒扫描的命令行工具，但同时也有支持图形界面的 ClamTK 工具

```bash
yum install clamav clamav-update -y
freshclam	# 更新病毒库
clamscan /home/xxx.test	# 扫描文件
```

#### 2. Linux Malware Detect

Linux Malware Detect 是采用GPL v2许可证发布的一款恶意软件扫描工具，专门为主机托管环境而设计。

##### LMD安装过程

```
wget http://www.rfxn.com/downloads/maldetect-current.tar.gz
tar -zvxf maldetect-current.tar.gz
cd maldetect-1.6.4
./install.sh
```



### 4. 云安全

#### WAF

Web应用防火墙（WAF）对网站或者APP的业务流量进行恶意特征识别及防护，将正常、安全的流量回源到服务器。避免网站服务器被恶意入侵，保障业务的核心数据安全，解决因恶意攻击导致的服务器性能异常问题。

