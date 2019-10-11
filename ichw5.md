# 第五次計概作業

## 北京大学某单位的某台机器IP地址为162.105.80.160, 子网掩码为255.255.255.192，

### 1) 该单位的网络号(网络+子网)是多少？
> 首先162.105.80.160——> 1010 0010 0110 0101 0101 0000 1010 0000
      255.255.255.19——>1111 1111 1111 1111 1111 1111 1100 1000
> 进行按位与运算后得出结果为：162.105.80.128
  所以网络号为162.105.80.128
  
### 2) 该单位理论上可容纳多少主机？
> 理论上可容纳62个主机。

### 3) 北大可以有多少个这样的子网(假定北大全部是162.105网段)？
> IP地址前后两段后面的数字均被用于划分分子网
  网络位有26位（1111 1111 1111 1111 1111 1111 1100 0000）
  B类基础位为16位（1010 0010 0110 1001 0000 0000 0000 0000 ）
  可以有2^10=1024个子网

## 2.解释TCP协议建立连接为什么设计为三步握手（3-way handshake）？
> TCP是什么？

> TCP(Transmission Control Protocol 传输控制协议)是一种面向连接的、可靠的、基于字节流的传输层通信协议。            
 在简化的计算机网络OSI模型中，它完成第四层传输层所指定的功能，用户数据报协议(UDP)是同一层内另一个重要的传输协议。         
 在因特网协议族(Internet protocol suite)中，TCP层是位于IP层之上，应用层之下的中间层。             
 不同主机的应用层之间经常需要可靠的、像管道一样的连接，但是IP层不提供这样的流机制，而是提供不可靠的包交换。             

>TCP的机制需要准备？
 
> B建立类似操作，TCP连接的一方A由系统随机设定一个32位长的序列号（Initial Sequence Number），假设A的初始序列号为1000，以该序列号为原点，对自己将要发送的每个字节的数据进行编号，1001，1002，1003…，并把自己的初始序列号ISN告诉B，让B有一个思想准备，什么样编号的数据是合法的，什么编号是非法的，比如编号900就是非法的，同时B还可以对A每一个编号的字节数据进行确认。如果A收到B确认编号为2001，则意味着字节编号为1001-2000，共1000个字节已经安全到达。同理，B也要做如上准备，选取一个序列号，并把序列号告诉A。

> 如何建立连接协议-三次握手？
  在TCP/IP协议中，TCP协议提供可靠的连接服务，采用三次握手建立一个连接：
> 1）第一次握手：建立连接时，客户端A主动向服务器B发送SYN包，并进入SYN_SEND状态，等待服务器B确认；
  2）第二次握手：服务器B收到客户端A发送的SYN包，必须确认客户端A的SYN，同时自己也发送一个SYN包，即SYN+ACK包，此时服务器B进入SYN_RECV状态；
  3）第三次握手：客户端A收到服务器B的SYN+ACK包，向服务器B发送确认包ACK，此包发送完毕，客户端A进入ESTABLISHED状态，完成三次握手。

> 如果最后一次B没有收到A的包应该怎么办

**第一个包，即A发给B的SYN 中途被丢，没有到达B**
  A会周期性超时重传，直到收到B的确认

**第二个包，即B发给A的SYN +ACK 中途被丢，没有到达A**
  B会周期性超时重传，直到收到A的确认

**第三个包，即A发给B的ACK 中途被丢，没有到达B**
A发完ACK，单方面认为TCP为 Established状态，而B显然认为TCP为Active状态

> a. 假定此时双方都没有数据发送，B会周期性超时重传，直到收到A的确认，收到之后B的TCP 连接也为 Established状态，双向可以发包。
 b. 假定此时A有数据发送，B收到A的 Data + ACK，自然会切换为established 状态，并接受A的 Data。
 c. 假定B有数据发送，数据发送不了，会一直周期性超时重传SYN + ACK，直到收到A的确认才可以发送数据。
 > 因此，建立三次握手，就可以实现建立状态。
 
 ## 有哪些恶意软件, 如何防范恶意软件？
 
**蠕虫**

  蠕虫病毒是一种常见的计算机病毒。它是利用网络进行复制和传播，传染途径是通过网络和电子邮件。最初的蠕虫病毒定义是因为在DOS环境下，病毒发作时会在屏幕上出现一条类似虫子的东西，胡乱吞吃屏幕上的字母并将其改形。蠕虫病毒是自包含的程序（或是一套程序），它能传播自身功能的拷贝或自身的某些部分到其他的计算机系统中（通常是经过网络连接）。

**木马**

  木马（Trojan）,也称木马病毒，是指通过特定的程序（木马程序）来控制另一台计算机。木马通常有两个可执行程序：一个是控制端，另一个是被控制端。木马这个名字来源于古希腊传说（荷马史诗中木马计的故事，Trojan一词的特洛伊木马本意是特洛伊的，即代指特洛伊木马，也就是木马计的故事）。“木马”程序是目前比较流行的病毒文件，与一般的病毒不同，它不会自我繁殖，也并不“刻意”地去感染其他文件，它通过将自身伪装吸引用户下载执行，向施种木马者提供打开被种主机的门户，使施种者可以任意毁坏、窃取被种者的文件，甚至远程操控被种主机。

**广告软件**

  是指以一个附带广告的电脑程序，以广告作为盈利来源的软件。此类软件往往会强制安装并无法卸载；在后台收集用户信息牟利，危及用户隐私；频繁弹出广告，消耗系统资源，使其运行变慢等。

>如何防范？

>1.安装杀毒软件/安全防护软件, 及时打补丁2.使用防火墙, 禁止外部计算机通过网络访问本机
3.不随便下载运行可执行程序4.不打开未知的邮件附件
5.U 盘 通常带毒, 打开前要先查毒6.不随便暴露自己的 email、生日、手机等重要信息
7.不以 Administrator 权限操作计算机