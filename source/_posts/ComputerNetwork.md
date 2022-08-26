---
title: 计网学习笔记
date: 2021-11-13 10:18:48
index_img: ../picture/20211113102222.jpg
banner_img: ../picture/20211113102251.jpg
math: true
tags: 计算机网络
categories: 计算机基础
---

# 因特网概述

- 网络（Network）由若干**结点**（Node）和连接这些结点的**链路**（Link）组成。
- 多个网络还可以通过路由器互连起来，这样就构成了一个覆盖范围更大的网络，即互联网。
- 因特网（Internet）是世界上最大的互联网络（用户数以亿计，互连的网络数以百万计）。

![因特网发展的三个阶段](ComputerNetwork/20211101192730.png)

> ISP（Internet Service Provider）因特网服务提供者，普通用户接入因特网的过程就是通过ISP。
>
> ISP可以从因特网管理机构申请到成块的IP地址，同时拥有通信线路以及路由器等连网设备。任何机构或个人只要向ISP缴纳费用，就可以从ISP得到所需要的IP地址。（因特网上的主机必须有IP地址才能通信）

![基于ISP的三层结构的因特网示意图](ComputerNetwork/20211101193403.png)

**因特网组成：**

- 边缘部分
  - 由所有连接在因特网上的主机组成。这部分是用户直接使用的，用来进行通信（传送数据、音频或视频）和资源共享。
- 核心部分
  - 由大量网络和连接这些网络的路由器组成。这部分是为边缘部分提供服务的（提供连通性和交换）。

![因特网的组成](ComputerNetwork/20211101194132.png)

# 三种交换方式

## 电路交换（Circuit Switching）

- 电话交换机接通电话线的方式称为电路交换
- 从通信资源的分配角度来看，交换就是按照某种方式动态地分配传输线路的资源
- 电路交换的三个步骤：
  - 建立连接（分配通信资源）
  - 通话（一直占用通信资源）
  - 释放连接（归还通信资源）

当使用电路交换来传送计算机数据时，其线路的传输效率往往很低。

## 分组交换（Packet Switching）

- 发送方：构造分组，发送分组
- 路由器：缓存分组，转发分组（存储转发）
- 接收方：接收分组，还原报文

![分组交换](ComputerNetwork/20211101194820.png)

## 报文交换（Message Switching）

也采用存储转发的方式



![三种交换的对比](ComputerNetwork/20211101195225.png)

**三种交换的对比：**

|          | 优点                                                         | 缺点                                                         |
| :------: | :----------------------------------------------------------- | :----------------------------------------------------------- |
| 电路交换 | 1. 通信时延小<br />2. 有序传输<br />3. 没有冲突<br />4. 适用范围广<br />5. 实时性强<br />6. 控制简单 | 1. 建立连接时间长<br />2. 线路独占，使用效率低<br />3. 灵活性差<br />4. 难以规格化 |
| 报文交换 | 1. 无需建立连接<br />2. 动态分配线路<br />3. 提高线路可靠性<br />4. 提高线路利用率<br />5. 提供多目标服务 | 1. 引起了转发时延<br />2. 需要较大的存储缓存空间<br />3. 需要传输额外的信息量 |
| 分组交换 | 1. 无需建立连接<br />2. 线路利用率高<br />3. 简化了存储管理<br />4. 加速传输<br />5. 减少出错概率和重发数据量 | 1. 引起了转发时延<br />2. 需要传输额外的信息量<br />3. 对于数据报服务，存在失序、丢失或虫回复分组的问题；<br />    对于虚电路服务，存在呼叫建立、数据传输和虚电路释放三个过程 |



# 计算机网络

## 定义

最简单的定义：一些**互连**、**自治**的计算机的集合。

计算机网络较好的定义是：计算机网络主要是由一些**通用的、可编程的硬件**互连而成的，而这些硬件并非专门用来实现某一特定目的（例如，传送数据或视频信号）。这些可编程的硬件能够用来**传送多种不同类型的数据**，并能**支持广泛的和日益增长的应用**。

## 分类

- 按交换技术分：电路交换网络、报文交换网络、分组交换网络
- 按使用者分：公用网、专用网
- 按传输介质分：有线网络、无线网络
- 按覆盖范围分：广域网`WAN`、城域网`MAN`、局域网`LAN`、个域网`PAN`
- 按拓扑结构分：总线型网络、星型网络、环型网络、网状型网络

## 计算机网络的性能指标

- 速率
- 带宽
- 吞吐量
- 时延
  - 发送时延 = 分组长度（b）/ 发送速率（b/s）
  - 传播时延 = 信道长度（m）/ 电磁波传播速率（m/s）
  - 处理时延：一般不便于计算，忽略
- 时延带宽积
  - 时延带宽积  = 传播时延 x 带宽
- 往返时间
- 利用率
  - 信道利用率：用来表示某信道有百分之几的时间是被利用的（有数据通过）
  - 网络利用率：全网络的信道利用率的加权平均
- 丢包率

## 计算机网络体系结构

![计算机网络体系结构](ComputerNetwork/20211101202615.png)

![常见的加算计网络体系结构](ComputerNetwork/20211101202742.png)

## 计算机网络体系结构分层的必要性

- 应用层：解决通过应用进程的交互来实现特定网络应用的问题
- 运输层：解决进程之间基于网络发通信问题
- 网络层：解决分组在多个网络上传输（路由）的问题
- 数据链路层：解决分组在一个网络（或一段链路）上传输的问题
- 物理层：解决使用何种信号来传输比特的问题

## 计算机网络中的专用术语

- 实体：任何可发送或接收信息的硬件或软件进程

  - 对等实体：收发双方相同层次中的实体

- 协议：控制两个对等实体进行逻辑通信的规则的集合

  - 三要素：语法、语义、同步

  语法：定义所交换信息的格式

  语义：定义收发双方所要完成的操作

  同步：定义收发双方的时序关系

- 服务：在协议的控制下，两个对等实体间的逻辑通信使得本层能够向上一层提供服务

- 服务访问点：在同一系统中相邻两层的实体交换信息的逻辑接口，用于区分不同的服务类型

  - 数据链路层的服务访问点为帧的“类型”字段。
  - 网络层的服务访问点为IP数据报首部中的“协议字段”。
  - 运输层的服务访问点为“端口号”。

- 服务原语：上层使用下层所提供的服务必须通过与下层交换一些命令，这些命令称为服务原语。

- 协议数据单元`PDU`：对等层次之间传送的数据包称为该层的协议数据单元。

- 服务数据单元`SDU`：同一系统内，层与层之间交换的数据包称为服务数据单元。

- 多个`SDU`可以合成为一个`PDU`；一个`SDU`也可划分为几个`PDU`。

==协议是”水平的“，服务是”垂直的“。==

![上述专业术语示意图](ComputerNetwork/20211101205703.png)



# 物理层

## 基本概念

物理层考虑的是怎样才能在连接各种计算机的传输媒体上传输数据比特流。

## 物理层协议的主要任务

- 机械特性：指明接口所用接线器的**形状**和**尺寸**、**引脚数目**和**排列**、**固定**和**锁定**装置。
- 电气特性：指明在接口电缆的各条线上出现的**电压的范围**。
- 功能特性：指明某条线上出现的某一电平的**电压表示何种意义**。
- 过程特性：指明对于不同功能的各种可能**事件的出现顺序**。

## 物理层下面的传输媒体

 导引型传输媒体：同轴电缆、双绞线、光纤、电力线

非导引型传输媒体：无线电波、微波、红外线、可见光

## 传输方式

- 串行传输

- 并行传输

  

- 同步传输

  收发双方时钟同步的方法

  - 外同步：在收发双方之间添加一条单独的时钟信号线
  - 内同步：发送端将时钟同步信号编码到发送数据中一起传输（例如曼彻斯特编码）

- 异步传输

  - 字节之间异步（字节之间的时间间隔不固定）
  - 字节中的每个比特仍然要同步（各比特的持续时间是相同的）



- 单向通信（单工）
- 双向交替通信（半双工）
- 双向同时通信（全双工）

## 信道的极限容量

奈氏准则：在假定的理想条件下，为了避免码间串扰，码元传输速率是有上限的    （W指带宽）

![奈氏准则](ComputerNetwork/20211101213359.png)

香农公式：

![香农公式](ComputerNetwork/20211101213026.png)

在信道带宽一定的情况下，根据奈氏准则和香农公式，要想提高信息的传输速率就必须采用**多元制**（更好的调制方法）和努力**提高信道中的信噪比**。

## 编码与调制

![常用编码](ComputerNetwork/20211103091136.png)



# 数据链路层

![数据链路层在网络体系结构中所处的地位](ComputerNetwork/20211103091459.png)

**链路（Link）**就是从一个结点到相邻结点的一段物理线路，而中间没有任何其他的交换结点。

**数据链路（Data Link）**是指把实现通信协议的硬件和软件加到链路上，就构成了数据链路。

数据链路层以**帧**为单位传输和处理数据。

![数据链路层](ComputerNetwork/20211103091608.png)

## 概述

使用点对点信道的数据链路层的三个重要问题

- 封装成帧
- 差错检测
- 可靠传输

尽管误码是不能完全避免的，但若能实现发送方发送什么，接收方就能收到什么，就称为可靠传输。

使用广播信道的数据链路层

- 共享式以太网的媒体接入控制协议`CSMA/CD`
- 802.11局域网的媒体接入控制协议`CSMA/CA`

数据链路层的互连设备

- 网桥和交换机的工作原理
- 集线器（物理层互连设备）与交换机的区别

## 封装成帧

封装成帧是指数据链路层给上层交付的协议数据单元添加帧头和帧尾使之称为帧。

- 帧头和帧尾中包含有重要的控制信息
- 帧头和帧尾的作用之一就是**帧定界**

透明传输是指**数据链路层对上层交付的传输数据没有任何限制**，就好像数据链路层不存在一样。

（即数据部分含有与帧首尾相同的字符或比特，此时应该加上转义字符）

- 面向字节的物理链路使用字节填充（或称字符填充）的方法实现透明传输
- 面向比特的物理链路使用比特填充的方法实现透明传输

为了提高帧的传输效率，应当使**帧的数据部分的长度尽可能大些**。

考虑到差错控制等多种因素，每一种数据链路层协议都规定了帧的数据部分的长度上限，即**最大传送单元MTU**（Maximum Transfer Unit）。

![帧](ComputerNetwork/20211103095110.png)

## 差错检测

实际的通信链路都不是理想的，比特在传输过程中可能会产生差错：1可能会变成0，而0也可能变成1。这称为**比特差错**。

在一段时间内，传输错误的比特占所传输比特总数的比率称为**误码率BER**（Bit Error Rate）。

使用**差错检测码**来检测数据在传输过程中是否产生了比特差错，是数据链路层所要解决的重要问题之一。



**奇偶校验**

- 在待发送的数据后面**添加1位奇偶校验位**，使整个数据（包括所添加的校验位在内）中**“1”的个数**为奇数（奇校验）或偶数（偶校验）。
- 如果有**奇数个位发生误码**，则奇偶性发生变化，**可以检查出误码**；
- 如果有**偶数个位发生误码**，则奇偶性发生变化，**不能检查出误码（漏检）**；

![奇校验和偶校验](ComputerNetwork/20211103100000.png)

**循环冗余校验CRC（Cyclic Redundancy Check）**

- 收发双方约定好一个**生成多项式G(x)**；
- 发送方基于待发送的数据和生成多项式计算出差错检测码（**冗余码**），将其添加到待传输数据的后面一起传输；
- 接收方通过生成多项式来计算收到的数据是否产生了误码；

![循环冗余校验CRC](ComputerNetwork/20211103100811.png)



**检错码**只能检测出帧在传输过程中出现了差错，但并不能定位错误，因此无法**纠正错误**。

要想纠正传输中的差错，可以使用冗余信息更多的**纠错码**进行**前向纠错**。但纠错码的开销比较大，在**计算机网络中较少使用**。

循环冗余校验**CRC**有很好的检错能力（**漏检率非常低**），虽然计算比较复杂，但非常**易于用硬件实现**，因此被**广泛应用于数据链路层**。

## 可靠传输

- 使用**差错检测技术**（例如循环冗余校验CRC），接收方的数据链路层就可检测出帧在传输过程中是否产生了**误码**（比特错误）。

- 数据链路层向上提供的服务类型

  - **不可靠传输服务**：**仅仅丢弃有误码的帧**，其他什么也不做；
  - **可靠传输服务**：想办法实现**发送端发送什么**，**接收端就收到什么**。

- 一般情况下，**有线链路**的误码率比较低，为了减小开销，并**不要求数据链路层**向上提供可靠传输服务。即使出现了误码，**可靠**传输的问题由其上层处理。

- **无线链路**易受干扰，误码率比较高，因此**要求数据链路层**必须向上层提供**可靠**传输服务。

- **比特差错**只是传输差错中的一种。

- 从整个计算机网络体系结构来看，传输差错还包括**分组丢失**、**分组失序**以及**分组重复**。

- 分组丢失、分组失序以及分组重复这些传输差错，一般不会出现在数据链路层，而会出现在其上层。

- **可靠传输服务并不仅局限于数据链路层**，其他各层均可选择实现可靠传输。

  ![可靠传输](ComputerNetwork/20211103104455.png)

- 可靠传输的实现比较复杂，开销也比较大，是否使用可靠传输取决于应用要求。

### 可靠传输的实现机制 -- 停止-等待协议SW

![停止-等待协议SW](ComputerNetwork/20211103203228.png)

【注意事项】

- 接收端检测到数据分组有误码时，将其丢弃并等待发送方的超时重传。但对于误码率较高的点对点链路，为使发送方**尽早重传**，也可**给发送方发送NAK分组**。
- 为了让接收方能够判断所收到的数据分组是否是重复的，需要给**数据分组编号**。由于停止-等待协议的停等特性，**只需1个比特编号**就够了，即编号0和1。
- 为了让发送方能够判断所收到的ACK分组是否是重复的，需要给**ACK分组编号**，所用比特数量**与数据分组编号所用比特数量一样**。数据链路层一般不会出现ACK分组迟到的情况，因此在**数据链路层实现停止-等待协议可以不用给ACK分组编号**。
- 超时计时器设置的**重传时间**应仔细选择。一般可将重传时间选为**略大于“从发送方到接收方的平均往返时间”**。
  - 在数据链路层点对点的往返时间比较确定，重传时间比较好设定。
  - 然而在运输层，由于端到端往返时间非常不确定，设置合适的重传时间有时并不容易。
- 当往返时延`RTT`远大于数据帧发送时延`TD`时（例如使用卫星链路)，信道利用率非常低。

停止-等待协议的信道利用率如下（一般`TA`远小于`TD`）
$$
U = \frac{T_D}{T_D + RTT + T_A} \approx \frac{T_D}{T_D + RTT}
$$
![信息传输示意图](ComputerNetwork/20211103204247.png)

### 可靠传输的实现机制 -- 回退N帧协议GBN（Go-Back-N）

![无差错情况](ComputerNetwork/20211104091957.png)

![累积确认（ACK1丢失）](ComputerNetwork/20211104093038.png)

![有差错情况](ComputerNetwork/20211104093428.png)

在有差错情况中，尽管序号为6，7，0，1的数据分组正确到达接受方，但由于5号数据分组误码不被接受，它们也“受到牵连”而不被接受，发送方还要重传这些数据分组，这就是所谓的`Go-back-N`（回退N帧）。

回退N帧协议在流水线传输的基础上利用发送窗口来限制发送方连续发送数据分组的数量，是一种连续ARQ协议。

可见，当通信线路质量不好的时候，回退N帧协议的信道利用率并不比停止-等待协议高。

![WT超过取值范围时](ComputerNetwork/20211104094207.png)

【小结】

**发送方**

- 发送窗口尺寸`WT = 1`时，为停止-等待协议，`WT > 2^n - 1`时，接收方会无法分辨新旧数组。
- 发送方只有收到对已发送数据分组的确认时，发送窗口才能向前相应滑动。
- 发送方收到多个重复确认时，可在重传计时器超时前尽早开始重传，由具体实现决定。

**接收方**

- 接收方的接收窗口尺寸`WR`的取值范围是`WR = 1`，因此接收方只能按序接收数据分组。
- 接收方可以连续收到好几个按序到达且无误码的数据分组后，才针对最后一个数据分组发送确认分组，称为累积确认。
- 接收方收到未按序到达的数据分组，除丢弃外，还要对最近按序接收的数据分组进行确认。

### 可靠传输的实现机制 -- 选择重传协议SR

**回退N帧协议**的接收窗口尺寸**`WR`只能等于1**，一个数据分组的误码会导致后续多个数据分组不能被接收而丢弃，会造成对通信资源的浪费。为了提高性能，可以设法只重传出现误码的数据分组。因此，接收窗口的尺寸**`WR`应大于1**，以便**接收方先收下失序到达但无误码并且序号落在接收窗口内的那些数据分组**，等到所缺分组收齐后再一并送交上层。这就是**选择重传协议**。

窗口尺寸要求：

- 发送方的发送窗口尺寸`WT`必须满足 `1 < WT < 2^(n-1)`，其中`n`是构成分组序号的比特数量
  - 若`WT = 1` ：与停止-等待协议相同
  - 若`WT > 2^(n-1)`：造成接收方无法分辨新、旧数据分组的问题
- 接收方的接收窗口尺寸`WR`必须满足`1 < WR <= WT`
  - 若`WR = 1`：与回退`N`帧协议相同
  - 若`WR > WT`：无意义

【小结】

**发送方**

- 发送窗口尺寸`WT = 1`时，为停止-等待协议，`WT > 2^(n-1)`时，接收方会无法分辨新旧数组。
- 发送方可在未收到接收方确认分组的情况下，将序号落在发送窗口内的多个数据分组全部发送出去。
- 发送方只有按序收到对已发送数据分组的确认时，发送窗口才能向前相应滑动。

**接收方**

- 接收方的接收窗口尺寸`WR`必须满足`1 < WR <= WT`
- **选择重传协议**为了使发送方仅重传出现差错的分组，接收方**不能再采用累积确认**，而需要对每个正确接受到的数据分组进行**逐一确认**。
- 接收方只有在按序接收数据分组后，接收窗口才能向前相应滑动。

## 点对点协议PPP

点对点协议`PPP（Point-to-Point Protocol）`是目前使用最广泛的点对点数据链路层协议。

![用户接入因特网](ComputerNetwork/20211104104920.png)

`PPP`协议为在点对点链路传输各种协议数据报提供了一个标准方法，主要由以下三部分组成：

- 对各种协议数据包的封装方法（封装成帧）
- 链路控制协议`LCP`                用于建立、配置以及测试数据链路的连接
- 一套网络控制协议`NCPs`      其中的每一个协议支持不同的网络层协议

![帧格式](ComputerNetwork/20211104105817.png)

实现透明传输：

- 面向字节的异步链路：字节填充法，插入“转义字符”
- 面向比特的同步链路：比特填充法，插入“比特0”

实现差错检测：接收方每收到一个`PPP`帧，就进行`CRC`检验。若`CRC`检验正确，就收下这个帧；反之丢弃。使用`PPP`的数据链路层**向上不提供可靠传输服务**。

![工作状态](ComputerNetwork/20211104110637.png)

## 媒体接入控制

共享信道要着重考虑的一个问题就是如何协调多个发送和接收站点对一个共享传输媒体的占用，即**媒体接入控制MAC**（Medium Access Control）。

![分类](ComputerNetwork/20211104111034.png)

随机接入

- 总线局域网使用的协议：`CSMA/CD`
- 无线局域网使用的协议：`CSMA/CA`

## MAC地址、IP地址以及ARP协议

- `MAC`地址是以太网的`MAC`子层所使用的地址；（数据链路层）
- `IP`地址是`TCP/IP`体系结构网际层所使用的地址； （网际层）
- `ARP`协议属于`TCP/IP`体系结构的网际层，其作用是，已知设备所分配到的`lP`地址使用`ARP`协议可以通过该`IP`地址获取到设备的`MAC`地址； （网际层）

### MAC地址

- 多个主机连接在同一广播信道上时，实现通信每个主机必须有一个唯一的标识，即一个数据链路层地址。
- 每个主机发送的**帧中必须携带标识发送主机和接收主机的地址**。由于这类地址是用于媒体接入控制`MAC(Media Access Control)`，因此被称为`MAC`地址。
  - `MAC`地址一般被固化在网卡（网络适配器）的电可擦可编程只读存储器`EEPROM`中，因此`MAC`地址也被称为**硬件地址**
  - `MAC`地址也被称为**物理地址**。但是不表示`MAC`地址属于物理层！
- 一般主机会有两个网络适配器：有线局域网适配器（有线网卡）和无限局域网适配器（无线网卡）。每个网络适配器有一个全球唯一的`MAC`地址。而交换机和路由器有更多的网络接口，所以会有更多的`MAC`地址。所以严格来说，**`MAC`地址是对网络上各接口的唯一标识，而不是对网络上各设备的唯一标识**。

![IEEE 802局域网的MAC地址格式](ComputerNetwork/20211104114750.png)

### IP地址

`IP`地址是因特网上的主机和路由器使用的地址，用于标识两部分信息：

- 网络编号：标识因特网上数以百万计的网络
- 主机编号：标识同一网络上不同主机（或路由器各接口）

![IP地址示意图](ComputerNetwork/20211104115843.png)

显然`MAC`地址是没有区分不同网络的功能的

- 如果只是一个单独的网络，不接入因特网，可以只使用`MAC`地址
- 如果主机要接入因特网，则`IP`地址和`MAC`地址都需要使用

![数据包转发过程中IP地址与MAC地址的变化情况](ComputerNetwork/20211104120553.png)

由上图可得数据包转发过程中源`IP`地址和目的`IP`地址保持**不变**，源`MAC`地址和目的`MAC`地址逐个链路（或逐个网络）**改变**。

### ARP协议

- 源主机在自己的**`ARP`高速缓存表**中查找目的主机的`IP`地址所对应的`MAC`地址，若找到了，则可以封装`MAC`帧进行发送；若找不到，则**发送`ARP`请求**（封装在广播`MAC`帧中）；
- 目的主机收到`ARP`请求后，将源主机的`IP`地址与`MAC`地址记录到自己的`ARP`高速缓存表中，然后给源主机发送**`ARP`响应（封装在单播`MAC`帧中）**，`ARP`响应中包含有目的主机的`IP`地址和`MAC`地址；
- `ARP`的作用范围：**逐段链路**或**逐个网络**使用；
- 除`ARP`请求和响应外，`ARP`还有其他类型的报文（例如用于检查`IP`地址冲突的“无故`ARP`、免费`ARP(Gratuitous ARP)`”）;
- `ARP`没有安全验证机制，**存在`ARP`欺骗（攻击）问题**。

![ARP请求报文传递过程](ComputerNetwork/20211104145654.png)

![ARP响应报文传递过程](ComputerNetwork/20211104145829.png)

`ARP`高速缓存表中的地址有两种类型：

- 动态：自动获取，生命周期默认为2分钟
- 静态：手工设置，不同操作系统下的生命周期不同，例如系统重启后不存在或者系统重启后依然有效

## 集线器与交换机的区别

| 集线器HUB（淘汰）                                            | 交换机SWITCH                                                 |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| 1. 早期以太网的互连设备<br />2. 工作在`OSI`体系结构的物理层<br />3. 对接收到的信号进行放大、转发<br />4. 使用集线器作为互连设备的以太网仍然术语共享总线式以太网。集线器互连起来的所有主机共享总线带宽，属于同一个碰撞域和广播域 | 1. 目前以太网中使用最广泛的互连设备<br />2. 工作在`OSI`体系结构的数据链路层（也包括物理层）<br />3. 根据`MAC`地址对帧进行转发<br />4. 使用交换机作为互连设备的以太网，称为交换式以太网。交换机可以根据`MAC`地址过滤帧，即隔离碰撞域<br />5. 交换机的每个接口是一个独立的碰撞域<br />6. 交换机隔离碰撞域但不隔离广播域（`VLAN`除外） |

## 以太网交换机自学习和转发帧的流程

1. 收到帧后进行**登记**。登记的内容为**帧的源`MAC`地址**及进入交换机的**接口号**
2. 根据**帧的目的`MAC`地址**和交换机的**帧交换表**对帧进行**转发**，有以下三种情况：
   1. **明确转发**：交换机知道应该从哪个（或哪些）接口转发该帧（单播，多播，广播）
   2. **盲目转发**：交换机不知道应该从哪个端口转发帧，只能将其通过除进入交换机的接口外的其他所有接口转发（也称为泛洪）
   3. **明确丢弃**：交换机知道不应该转发该帧，将其丢弃

![A->B](ComputerNetwork/20211104153532.png)

![B->A](ComputerNetwork/20211104153630.png)

![E->A](ComputerNetwork/20211104153742.png)

![G->A](ComputerNetwork/20211104153920.png)

【注意】

帧交换表中的每一条记录都有自己的**有效时间**，到期自动删除！这是因为**`MAC`地址与交换机接口的关系并不是永久性的**！

原因如下：

- 交换机的接口改接了另一台主机
- 主机更换了网卡

## 以太网交换机的生成树协议STP

如何提高以太网的可靠性？

添加**冗余链路**可以，但会带来负面效应——形成**网络环路**，网络环路会带来以下问题：

- 广播风暴（重复转发套娃）

  大量消耗网络资源，使得网络无法正常转发其他数据帧

- 主机收到重复的广播帧

  大量消耗主机资源

- 交换机的帧交换表震荡（漂移）

以太网交换机使用**生成树协议**`STP(Spanning Tree Protocol)`，可以在增加冗余链路来提高网络可靠性的同时又**避免网络环路带来的各种问题**。

- 不论交换机之间采用怎样的物理连接，交换机都能**自动计算并构建一个逻辑上没有环路的网络**，其逻辑拓扑结构必须是树型的（无逻辑环路）
- 最终生成的树型逻辑拓扑要**确保连通整个网络**
- 当首次连接交换机或网络**物理拓扑发生变化**时（有可能是人为改变或故障），交换机都将进行**生成树的重新计算**

## 虚拟局域网VLAN

### 概述

网络中会频繁出现广播信息

- `TCP/IP`协议栈中的很多协议都会使用广播：
  - 地址解析协议`ARP`（已知`IP`地址，找出其相应的`MAC`地址）
  - 路由信息协议`RIP`（一种小型的内部路由协议）
  - 动态主机配置协议`DHCP`（用于自动配置`IP`地址）
- `NetBEUI`：`Windows`下使用的广播型协议
- `IPX/SPX`：`Novell`网络的协议栈
- `Apple Talk`：`Apple`公司的网络协议栈

分割广播域的方法

- 使用路由器，但成本较高
- 虚拟局域网`VLAN`技术

虚拟局域网`VLAN(Virtual Local Area Network)`是一种将局域网内的设备划分成与物理位置无关的逻辑组的技术，这些逻辑组具有某些共同的需求。

### 实现机制

1. **`IEEE 802.1Q`帧**

`IEEE 802.1Q`帧（也称`Dot One Q`帧）对以太网的`MAC`帧格式进行了扩展，插入了**4字节的`VLAN`标记**。

![普通MAC帧与插入标记后的MAC帧](ComputerNetwork/20211104162859.png)

`VLAN`标记的**最后 12 比特**称为**`VLAN`标识符`VID`**，它唯一地标志了以太网帧术语哪一个`VLAN`。

- `VID`的取值范围是 0 ~ 4095（0 ~ 2^12 - 1）
- 0 和 4095 都不用来表示`VLAN`，因此用于表示`VLAN`的**`VID`的有效取值范围是 1 ~ 4094**

**`802.1Q`帧是由交换机来处理的，而不是用户主机来处理的**。

- 当交换机**收到普通的以太网帧**时，会将其插入 4 字节的`VLAN`标记转变为`802.1Q`帧，简称“**打标签**”
- 当交换机**转发`802.1Q`帧**时，**可能**会删除其 4 字节`VLAN`标记转变为普通以太网帧，简称“**去标签**”

2. 交换机的端口类型

交换机的端口类型有以下三种：

- `Access`

  一般用于**连接用户计算机**，只能属于一个`VLAN`，端口的`PVID`值与端口所属`VLAN`的`ID`值相同（默认为1）。

  ![Access端口发送与接收处理方法](ComputerNetwork/20211104165120.png)

- `Trunk`

  一般用于**交换机之间或交换机与路由器之间的互连**，可以属于多个`VLAN`，用户可以设置端口的`PVID`值（默认为1）。

  ![Trunk端口发送与接收处理方法](ComputerNetwork/20211104165037.png)

- `Hybrid`

  华为交换机私有，既可用于连接用户计算机也能连接交换机和路由器，可以属于多个`VLAN`，`PVID`可设置（默认为1）。

  ![Hybrid端口发送与接收处理方法](ComputerNetwork/20211104165508.png)

交换机个端口的缺省`VLAN ID`

- 在思科交换机上称为`Native VLAN`，即本征`VLAN`
- 在华为交换机上称为`Port VLAN ID`，即端口`VLAN ID`，简记为`PVID`

# 网络层

## 概述

网络层的主要任务是**实现网络互连**，进而**实现数据包在各网络之间的传输**。

要实现网络层任务，需要解决以下主要问题：

- 网络层向运输层提供怎样的服务（“可靠传输”还是“不可靠传输”）
- 网络层寻址问题
- 路由选择问题

![示意图](ComputerNetwork/20211105162949.png)

## 网络层提供的两种服务

### 面向连接的虚电路服务

- **可靠通信由网络来保证**
- 必须建立**网络层的连接——虚电路`VC(Virtual Circuit)`**
- 通信双方**沿着已建立的虚电路发送数组**
- 目的主机的地址仅在连接建立阶段使用，之后每个**分组的首部只需携带一条虚电路的编号**（构成虚电路的每一段链路都有一个虚电路编号）
- 这种通信方式如果再使用可靠传输的网络协议，就可使所发送的分组最终正确到达接收方（无差错按序到达、不丢失、不重复)。
- **通信结束后，需要释放之前所建立的虚电路**

![面向连接的虚电路服务](ComputerNetwork/20211105165251.png)

### 无连接的数据报服务

- **可靠通信由用户主机来保证**
- **不需要建立网络层连接**
- **每个分组可走不同的路径**
- 每个分组的**首部必须携带目的主机的完整地址**
- 这种通信方式所传送的分组可能误码、丢失、重复和失序
- 由于**网络本身不提供端到端的可靠传输服务**，所以网络中路由器可以做的比较简单
- 因特网采用了这种设计思想，**将复杂的网络处理功能置于因特网的边缘（用户主机和其内部的运输层）**，而将相对简单的尽最大努力的分组交付功能置于因特网核心

![无连接的数据报服务](ComputerNetwork/20211105165419.png)

## IPv4地址

### 概述

`IPv4`地址就是给因特网上的**每一台主机（或路由器）的每一个接口**分配一个在全世界范围内是**唯一的32比特的标识符**。

`IPv4`地址的编址方法经理了下面3个历史阶段

- 分类编址
- 划分子网
- 无分类编址

32比特的`IPv4`地址不方便阅读、记录以及输入等，因此采用**点分十进制表示方法**以便用户使用。

![举例](ComputerNetwork/20211105170641.png)

### 分类编址

![分类编址的IPv4地址](ComputerNetwork/20211105170848.png)

【注意事项】

- 只有 A 类、B 类和 C 类地址可分配给网络中的主机或路由器的各接口
- 主机号为“全0”的地址是网络地址，不能分配给主机或路由器的各接口
- 主机号为“全1”的地址是广播地址，不能分配给主机或路由器的各接口

判断网络地址类型：

- 根据地址左起第一个十进制数的值，可以判断出网络类别（小于127的为A类，128~191的为B类，192~223的为C类）
- 根据网络类别，就可找出地址中的网络号部分和主机号部分（A类地址网络号为左起第一个字节，B类地址网络号为左起前两个字节，C类地址网络号为左起前三个字节）
- 以下三种情况的地址不能指派给主机或路由器接口
  - A 类网络号 0 和 127
  - 主机号为“全 0”，这是网络地址
  - 主机号为“全 1”，这是广播地址

特殊的`IP`地址

- `0.0.0.0`：本网络上的本主机，只能作为源`IP`地址，不能作为目的`IP`地址
- `127.0.0.1`：常用的环回测试地址
- `255.255.255.255`：只能作为目的地址使用，表示“只在本网络上进行广播（各路由器均不转发）”

### 划分子网

**32比特的子网掩码可以表明分类`IP`地址的主机号部分被借用了几个比特作为子网号**

- 子网掩码使用**连续的比特1来对应网络号和子网号**
- 子网掩码使用**连续的比特0来对应主机号**
- 将划分子网的**`IPv4`地址**与其对应的**子网掩码**进行**逻辑与运算**就可得到`IPv4`地址**所在子网的网络地址**

给定一个分类的`IP`地址和其相应的子网掩码，就可以得到子网划分的细节：

- 划分出的子网数量
- 每个子网可分配的`IP`地址数量
- 每个子网的网络地址（起始）和广播地址（结尾）
- 每个子网可分配的最小和最大地址

默认的子网掩码是指在未划分子网的情况下使用的子网掩码

![默认子网掩码](ComputerNetwork/20211105174723.png)

### 无分类编址

划分子网在一定程度上缓解了因特网在发展中遇到的困难，但是**数量巨大的 C 类网**因为其**地址空间太小**并**没有得到充分利用**。为此，提出了采用**无分类编址**的方法来解决`IP`地址紧张的问题。

1993 年发布了无分类域间路由选择`CIDR(Classles Inter-Domain Routing)`：

- `CIDR`消除了传统的 A 类、B 类和 C 类地址，以及划分子网的概念
- `CIDR`可以更加有效地分配`IPv4`的地址空间，并且可以在新的`IPv6`使用之前允许因特网的规模继续增长

`CIDR`使用“**斜线记法**”，或称`CIDR`记法。即在`IPv4`地址后面加上斜线“/”，在**斜线后面写上网络前缀所占的比特数量**

![举例](ComputerNetwork/20211105180252.png)

`CIDR`实际上是将网络前缀都相同的连续的IP地址组成一个“CIDR地址块”，我们只要知道`CIDR`地址块中的任何一个地址，就可以知道该地址块的全部细节。

**路由聚合**（构造超网）

![举例](ComputerNetwork/20211105195535.png)

- **网络前缀越长，地址块越小，路由越具体**
- 若路由器查表转发分组时发现有多条路由可选，则选择网络前缀最长的那条，这称为**最长前缀匹配**，因为这样的路由更具体

### 应用规划

有两种方法，分别是**定长的子网掩码**`FLSM(Fixed Length Subnet Mask)`和**变长的子网掩码**`VLSM(Variable Length Subnet Mask)`。

定长的子网掩码`FLSM`

- 使用同一个子网掩码来划分子网
- 每个子网多分配的`IP`地址数量相同，造成`IP`地址的浪费

变长的子网掩码`VLSM`

- 使用不同的子网掩码来划分子网
- 每个子网所分配的`IP`地址数量可以不同，尽可能减少对`IP`地址的浪费

![FLSM举例](ComputerNetwork/20211105201305.png)

![VLSM举例](ComputerNetwork/20211105201759.png)

## IP数据报的发送和转发过程

包含以下两部分：

- 主机发送`IP`数据报
- 路由器转发`IP`数据报

![间接交付--C向F发送数据报](ComputerNetwork/20211108093525.png)

当本网络中的主机要和其他网络中的主机进行通信时，会将`IP`数据报传输给默认网关，由默认网关即路由器帮主机将`IP`数据报转发出去。

![默认网关](ComputerNetwork/20211108093941.png)

路由器收到`IP`数据报后的转发过程：

- 检查`IP`数据报首部是否出错，若出错，则直接丢弃该`IP`数据报并通告源主机；若没有出错，则进行转发
- 根据`IP`数据报的目的地址在路由表中查找匹配的条目，若找到，则按条目转发；若找不到，则丢弃该`IP`数据报并通告源主机

## 静态路由配置

静态路由配置是指用户或网络管理员使用路由器的相关命令给路由器**人工配置路由表**。

- 这种人工配置方式简单、开销小。但不能及时适应网络状态（流量、拓扑等）的变化
- 一般只在小规模网络中采用

路由条目的类型

- 直连网络
- 静态路由（人工配置）
- 动态路由（路由选择协议）

特殊的静态路由条目

- 默认路由（目的网络为`0.0.0.0`，地址掩码为`0.0.0.0`）
- 特定主机路由（目的网络为特定主机的`IP`地址，地址掩码为`255.255.255.255`）
- 黑洞路由（下一跳为`null0`）

使用静态路由配置可能出现以下**导致**产生**路由环路**的错误

- 配置错误
- 聚合了不存在的网络
- 网络故障

![特定主机路由与默认路由](ComputerNetwork/20211108111831.png)

![路由环路举例1](ComputerNetwork/20211108112019.png)

为了防止`IP`数据报在路由环路中永久兜圈，在`IP`数据报首部设有生存时间`TTL`字段。`IP`数据报进入路由器后，`TTL`字段的值减1。若`TTL`的值不等于0，则被路由器转发，否则被丢弃。

![路由环路举例2](ComputerNetwork/20211108112857.png)

解决办法是在路由表中添加黑洞路由：

![添加黑洞路由](ComputerNetwork/20211108112953.png)

![路由环路举例3](ComputerNetwork/20211108113246.png)

解决办法也是在路由表中添加黑洞路由：

![添加黑洞路由](ComputerNetwork/20211108113337.png)

## 路由选择协议概述

| 静态路由选择                                                 | 动态路由选择                                                 |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| 1. 由**人工配置**的网络路由、默认路由、特定主机路由、黑洞路由等都属于静态路由<br />2. 人工配置方式简单、开销小。但不**能及时适应网络状态（流量、拓扑等）的变化**<br />3. 一般只在**小规模网络**中采用 | 1. 路由器通过路由选择协议**自动获取路由信息**<br />2. 比较复杂、开销比较大。**能较好地适应网络状态的变化**<br />3. 适用于**大规模网络** |

路由选择协议的主要特点：

- 自适应：动态路由选择，能较好地适应网络状态的变化
- 分布式：路由器之间交换路由信息
- 分层次：将整个因特网划分为许多较小的自治系统`AS(Atonomous System)`

![常见的路由选择协议](ComputerNetwork/20211108114958.png)

![路由器的基本结构](ComputerNetwork/20211108115519.png)

## IPv4数据报的首部格式

![IPv4数据报的首部格式](ComputerNetwork/20211108150845.png)

## 网际控制报文协议ICMP

为了更有效地转发`IP`数据报和提高交付成功的机会，在网际层使用了网际控制报文协议`ICMP(Internet Control Message Protocol)`。

主机或路由i去使用`ICMP`来发送**差错报告报文**和**询问报文**。 

**`ICMP`报文被封装在`IP`数据报**中发送。

`ICMP`差错报文共有五种： 

- 终点不可达

  路由器或主机不能交付数据报时，就向源点发送终点不可达报文。

- 源点抑制

  路由器或主机由于拥塞而丢弃数据报时，就向源点发送源点抑制报文。

- 时间超过

  路由器收到一个目的`IP`地址不是自己的`IP`数据报，会将其生存时间`TTL`字段的值减1。若结果不为0，则将该`IP`数据报转发出去；若结果为0，除丢弃该`IP`数据报后，还要向源点发送时间超过报文。

  另外，当终点在预先规定的时间内不能收到一个数据报的全部数据报片时，就把已收到的数据报片都丢弃，也会向源点发送时间超过报文。

- 参数问题

  路由器或目的主机收到`IP`数据报后，根据其首部中的检验和字段发现首部在传输过程中出现了误码，就丢弃该数据报，并向源点发送参数问题报文。

- 改变路由（重定向）

  路由器把改变路由报文发送给主机，让主机知道下次应将数据报发送给另外的路由器（可通过更好的路由）。

不应发送`ICMP`差错报告报文的情况：

- 对`ICMP`差错报告报文不再发送`ICMP`差错报告报文
- 对第一个分片的数据报片的所有后续数据报片都不发送`ICMP`差错报告报文
- 对具有多播地址的数据报都不发送`ICMP`差错报告报文
- 对具有特殊地址（如`127.0.0.1`或`0.0.0.0`）的数据报不发送`ICMP`差错报告报文

常用的`ICMP`询问报文：

- 回送请求报文

  `ICMP`回送请求报文是由主机或路由器向一个特定的目的主机发出的询问。收到此报文的主机必须给源主机或者路由器发送`ICMP`回送回答报文。**用来测试目的站是否可达**。

- 时间戳请求和回答

  `ICMP`时间戳请求报文是请某个主机或路由器回答当前的日期和时间。**用来进行时钟同步和测量时间**。

`ICMP`应用举例

- 分组网间探测`PING(Packet InterNet Groper)`

  - 用来测试主机或路由器间的连通性
  - 应用层直接使用网际层的`ICMP`（没有通过运输层的`TCP`或`UDP`）
  - 使用`ICMP`回送请求和回答报文

  ![ping示例](ComputerNetwork/20211108161305.png)

- 跟踪路由`traceroute`

  - 用来测试`IP`数据报从源主机到达目的主机要经过哪些路由器
  - Windows
    - tracert命令
    - 应用层直接使用网际层`ICMP`
    - 使用了`ICMP`回送请求报文和回答报文以及差错报告报文
  - Unix
    - traceroute命令
    - 在运输层使用`UDP`协议
    - 仅使用`ICMP`差错报告报文

  ![跟踪示例](ComputerNetwork/20211108161204.png)

## 虚拟专用网 VPN 与网络地址转换 NAT

虚拟专用网`VPN(Virtual Private Network)`

- 内联网`VPN`

  同一机构内不同部门的内部网络所构成的虚拟专用网`VPN`。 

- 外联网`VPN`

  一个机构的`VPN`需要有某些外部机构参加进来。

- 远程接入`VPN`

  在外网环境下运行`VPN`软件来与公司的主机建立`VPN`隧道，即可访问专用网络即内网中的资源。

![内联网VPN](ComputerNetwork/20211108162215.png)

![专用网络地址即本地地址](ComputerNetwork/20211108163115.png)



网络地址转换`NAT(Network Address Translation)`

`NAT`能使大量使用内部专用地址的专用网络用户共享少量外部全球地址来访问因特网上的主机和资源。

![网络地址转换NAT](ComputerNetwork/20211108163741.png)

这种转换方法会由于NAT路由器中的全球`IP`地址有限而受限，至多只能有对应数量的内网主机能够和因特网上的主机通信。

由于绝大多数的网络应用都是使用运输层协议`TCP`或`UDP`来传送数据，因此可以利用运输层的端口号和`IP`地址一起进行转换。这样用**一个全球`IP`地址**就可以使**多个本地主机**同时和因特网上的主机痛惜。这种将端口号和`IP`地址一起进行转换的技术叫做**网络地址与端口号转换`NAPT(Network Address and Port Translation)`**。

# 运输层

## 概述

- 物理层、数据链路层以及网络层它们共同解决了将主机通过异构网络互联起来所面临的问题，**实现了主机到主机的通信**。
- 实际上在计算机网络中进行**通信的真正实体是位于通信两端主机中的进程**。
- **如何为运行在不同主机上的应用进程提供直接的通信服务是运输层的任务**，运输层协议又称为端到端协议。

![示意图](ComputerNetwork/20211110103624.png)

![不同主机上的应用进程通信](ComputerNetwork/20211110103941.png)

运输层直接为应用进程间的逻辑通信提供服务。

根据应用需求的不同，**因特网的运输层**为应用层提供了两种不同的运输协议，即面向连接的`TCP`和无连接的`UDP`。

## 运输层端口号、复用与分用

- 运行在计算机上的进程使用**进程标识符**`PID`来标志。
- 不同的操作系统使用**不同格式的进程标识符**。
- 为了使不同操作系统的计算机的应用进程之间能够通信，就必须**使用统一的方法对`TCP\IP`体系的应用进程进行标识**。
- `TCP\IP`体系的运输层使用**端口号**来区分应用层的不同应用进程。
  - 端口号使用**16比特表示**，取值范围 **0~65535**；
    - 熟知端口号：0~1023，`TCP\IP`中最重要的一些应用协议，如：`FTP`使用 21/20，`HTTP`使用 80，`DNS`使用 53。
    - 登记端口号：1024~49151，为没有熟知端口号的应用程序使用。按规定手续登记，防止重复。如：`Microsoft RDP`微软远程桌面使用的端口是3389。
    - 短暂端口号：49252~65535，苦于给客户进程选择暂时使用。通信结束后可供其他客户进程使用。
  - **端口号只具有本地意义**，即端口号只是为了**标识本计算机应用层中的各进程**，在因特网中，**不同计算机中的相同端口号是没有联系的**。



发送方的复用和接收方的分用

![发送方的复用和接收方的分用](ComputerNetwork/20211110110441.png)

![TCP/IP体系的应用层常用协议所使用的运输层熟知端口号](ComputerNetwork/20211110110533.png)

## UDP 与 TCP 的对比

| 用户数据报协议UDP(User Datagram Protocol)                    | 传输控制协议TCP(Transmission Control Protocol)               |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| 1. 可随时发送数据，无连接的`UDP`<br />2. 支持单播、多播以及广播，即支持一对一，一对多，一对全的通信<br />3. `UDP`是面向应用报文的<br />4. `UDP`向上层提供无连接**不可靠的传输**服务（适用于`IP`电话、视频会议等实时应用）<br />5. `UDP`用户数据报首部仅8字节 | 1. 数据传输之前必须通过“三报文握手”建立连接，数据传输完成后必须通过“四报文挥手”释放连接，**面向连接的`TCP`**<br />2. 仅支持单播，即一对一通信，因为数据传输前需要建立连接<br />3. `TCP`是面向字节流的<br />4. `TCP`向上层提供面向连接的**可靠传输**服务（适用于要求可靠传输的应用，例如文件传输）<br />5. `TCP`报文段首部最小20字节，最大60字节 |

![UDP用户数据报与TCP报文段的首部对比](ComputerNetwork/20211110112746.png)

## TCP 的流量控制

所谓流量控制`(flow control)`就是**让发送方的发送速率不要太快，要让接收方来得及接收**。

利用**滑动窗口**机制可以很方便地在`TCP`连接上实现对发送方的流量控制。

![举例](ComputerNetwork/20211110114215.png)

![TCP死锁](ComputerNetwork/20211110114340.png)

**解决`TCP`死锁问题：**

`TCP`为每一个连接设有一个持续计时器。只要`TCP`连接的一方收到对方的零窗口通知，就启动持续计时器。若计时器超时，就发送一个零窗口探测报文，仅携带 1 字节的数据，对方在确认这个探测报文段时，给出自己现在的接收窗口值。如果仍然是0，那么收到这个报文段的一方就重新启动持续计时器，若不为0，死锁的局面就可以打破了。

若零窗口探测报文段丢失，也能打破死锁的局面，因为零窗口探测报文段也有重传计时器。当超时后，零窗口探测报文段会被重传。

## TCP 的拥塞控制

对网络中某一资源的需求超过了该资源所能提供的可用部分，网络性能就要变坏。这种情况就叫做**拥塞**`(congestion)`。

若出现拥塞而不进行控制，整个网络的吞吐量将随输入负荷的增大而下降。

![输入负载与吞吐量的关系](ComputerNetwork/20211110115714.png)

`TCP`的拥塞控制算法

- 慢开始`(slow-start)`
- 拥塞避免`(congestion avoidance)`
- 快重传`(fast retransmit)`
- 快恢复`(fast recovery)`

![慢开始和拥塞避免](ComputerNetwork/20211110120517.png)

- “慢开始”是指一开始向网络注入的报文段少，并不是指拥塞窗口`cwnd`增长速度慢

- “拥塞避免”并非是指完全能够避免拥塞， 而是指拥塞避免阶段将拥塞窗口控制为按线性规律增长，比较不容易出现拥塞

- 所谓快重传就是使发送方尽快进行重传，而不是等超时重传计时器超时再重传。

  - 接收方**立即发送确认**
  - 即使收到失序的报文段也要立即发出对已收到报文段的**重复确认**
  - 发送方一旦收到 3 个连续的重复确认，就将相应报文段**立即重传**，而不是等到超时重传

  ![示意图](ComputerNetwork/20211110121356.png)

- 发送方一旦收到 3 个重复确认，就可以知道只是丢失了个别报文段。故不启动慢开始算法，而**执行快恢复算法**

  - 发送方将慢开始门限`ssthresh`值和拥塞窗口`cwnd`值调整为当前窗口的一半；开始执行拥塞避免算法。
  - 也有的快恢复实现是把快恢复开始时的拥塞窗口`cwnd`值再增大一些，即等于新的`ssthresh + 3`
    - 接收到 3 个重复的确认表明有 3 个数据报文段已经离开了网络，因此可以适当扩大拥塞窗口

![4种算法](ComputerNetwork/20211110122059.png)

## TCP 超时重传时间的选择

![示意图](ComputerNetwork/20211110151246.png)

- 不能直接使用某次测量得到的`RTT`样本来计算超时重传时间`RTO`

- 利用每次测量得到的`RTT`样本，计算加权平均往返时间`RTTs`（又称为平滑的往返时间）

- 超时重传时间`RTO`应略大于加权平均往返时间`RTTs`

  

- 针对**出现超时重传时无法测准往返时间**`RTT`的问题，`Karn`提出了一个算法：在计算加权平均往返时间`RTTs`时，只要报文段重传了，就不采用其往返时间`RTT`样本。但这样会引起新的问题，如果报文段的时延突然增大了很多并且保持很长一段时间，那么在原有的重传时间内是收不到确认报文的，那么会反复重传报文。

- 因此对`Karn`算法进行修正：报文段每重传一次，就把超时重传时间`RTO`增大一些。典型做法是增大到原来的 2 倍。

## TCP 可靠传输的实现

`TCP`基于**以字节为单位的滑动窗口**来实现可靠传输。

![示意图](ComputerNetwork/20211112113930.png)

- 虽然发送方的发送窗口是根据接收方的接收窗口设置的，但在同一时刻，**发送方的发送窗口并不总是和接收方的接收窗口**一样大
  - 网络传送窗口值需要经历一定时间的滞后
  - 发生拥塞发送方需减小发送窗口尺寸
- 对于**不按序到达的数据应如何处理**，`TCP`无明确规定
  - 若一律丢弃，那么接收窗口的管理会比较简单，但这样对网络资源的利用不利，因为发送方会重复传送较多的数据
  - 通常是先临时存放在接收窗口中，等到字节流中所缺少的字节收到后，再**按序交付上层的应用进程**
- `TCP`要求接收方必须有**累计确认和捎带确认机制**，这样可以减小传输开销。接收方可以在合适的时候发送确认，也可以在自己有数据要发送时把确认信息顺便捎带上。
  - **接收方不应过分推迟发送确认**，否则会导致发送方不必要的超时重传，这反而会浪费网络资源。`TCP`标准规定，确认推迟的时间不应超过 0.5 秒
  - 捎带确认实际上很少发生，因为大多数应用程序很少同时在两个方向上发送数据
- **`TCP`的通信是全双工通信**。通信中的每一方都在发送和接收报文段。因此，每一方都有自己的发送窗口和接收窗口

## TCP 的运输连接管理

### TCP 的连接建立

- `TCP`是面向连接的协议，它基于运输连接来传送`TCP`报文段

- `TCP`运输连接的建立和释放是每一次面向连接的通信中必不可少的过程

- `TCP`运输连接有三个阶段，建立`TCP`连接、数据传送和释放`TCP`连接

  ![TCP连接的三个阶段](ComputerNetwork/20211112115950.png)

- `TCP`的运输连接管理就是使运输连接的建立和释放都能正常地进行

![TCP使用“三报文握手”建立连接](ComputerNetwork/20211112120425.png)

【注意】

- `TCP`标准规定`SYN = 1`的报文段不能携带数据，但要消耗掉一个序号
- `TCP`标准规定普通的确认报文段如果不携带数据，则不消耗序号

`TCP`客户进程最后发送一个普通的`TCP`确认报文段是否多余即是否可以使用两报文握手？

不多余，这是为了防止已失效的连接请求报文段突然又传送到了`TCP`服务器，因而导致错误。

![原因](ComputerNetwork/20211112120832.png)

### TCP 的连接释放

![TCP通过”四报文挥手“来释放连接](ComputerNetwork/20211112121839.png)

**`TCP`客户进程在发送完最后一个确认报文段后，进入时间等待状态是否有必要？**

有必要，因为发送的最后一个确认报文段可能会丢失，导致`TCP`服务器没有接收到进行超时重传，而此时若`TCP`客户端已进入关闭状态，则会收不到导致`TCP`服务器无法进入关闭状态。另外，`TCP`客户进程在发送完最后一个确认报文段后，再经过`2MSL`时长，就可以使本次连接持续时间内多产生的所有报文段都从网络中消失，这样就会使下一个`TCP`连接中不会出现就链接中的报文段。

![原因](ComputerNetwork/20211112122144.png)

**当`TCP`客户端出现故障时，`TCP`服务器如何发现？**

TCP服务器进程每收到一次TCP客户进程的数据，就重新设置并启动**保活计时器**（2小时定时）。

若保活计时器定时周期内未收到`TCP`客户进程发来的数据，则**当保活计时器到时后，`TCP`服务器进程就向`TCP`客户进程发送一个探测报文段**，以后则每隔75秒钟发送一次。若一连发送10个探测报文段后仍无`TCP`客户进程的响应，`TCP`服务器进程就认为`TCP`客户进程所在主机出了故障，接着就关闭这个连接。

## TCP 报文段的首部格式

![TCP 报文段的首部格式](ComputerNetwork/20211112200056.png)

- **源端口**：占16比特，写入源端口号，用来**标识发送该`TCP`报文段的应用进程**。
- **目的端口**：占16比特，写入目的端口号，用来**标识接收该`TCP`报文段的应用进程**。
- **序号**：占32比特，取值范围`[0, 2^32 - 1]`，序号增加到最后一个后，下一个序号就又回到0。**指出本`TCP`报文段数据载荷的第一个字节的序号**。
- **确认号**：占32比特，取值范围`[0, 2^32 - 1]`，确认号增加到最后一个后，下一个确认号就又回到0。**指出期望收到对方下一个`TCP`报文段的数据载荷的第一个字节的序号**，同时也是对之前收到的所有数据的确认。若确认号为 n ，则表明到序号`n - 1`为止的所有数据都已正确接收，期望接收序号为 n 的数据。
- **确认标志位`ACK`**：取值为1时确认号字段才有效；取值为0时确认号字段无效。`TCP`规定，在连接建立后所有传送的`TCP`报文段都必须把`ACK`置1。
- ![示意图](ComputerNetwork/20211112201509.png)
- **数据偏移**：占4比特，并以4字节为单位。用来**指出`TCP`报文段的数据载荷部分的起始处距离`TCP`报文段的起始处有多远**。这个字段实际上是指出了`TCP`报文段的首部长度。故数据偏移字段的最小值为`0101`（20 / 4），最大值为`1111`（60 / 4）。
- **保留**：占6比特，保留为今后使用，但目前应置为0。
- **窗口**：占16比特，以字节为单位。**指出发送本报文段的一方的接收窗口**。窗口值作为接收方让发送方设置其发送窗口的依据。这是以接收方的接收能力来控制发送方的发送能力，称为流量控制。
- **校验和**：占16比特，检查范围包括`TCP`报文段的首部和数据载荷两部分。在计算校验和时，要在`TCP`报文段的前面加上12字节的伪首部。
- **同步标志位`SYN`**：在`TCP`连接建立时用来同步序号。
- **终止标志位`FIN`**：用来释放`TCP`连接。
- **复位标志位`RST`**：用来复位`TCP`连接。当`RST = 1`时，标识`TCP`连接出现了异常，必须释放连接，然后再重新建立连接。`RST`置1还用来拒绝一个非法的报文段或拒绝打开一个`TCP`连接。
- **推送标志位`PSH`**：接受方的`TCP`收到该标志位为1的报文段会**尽快上交应用进程**，而不必等到接收缓存都填满后再向上交付。
- **紧急标志位`URG`**：取值为1时紧急指针字段有效；取值为0时紧急指针字段无效。
- **紧急指针**：占16比特，以字节为单位，用来指明紧急数据的长度。当发送方有紧急数据时，可将紧急数据插队到发送缓存的最前面，并立刻封装到一个`TCP`报文段中进行发送。
- **选项**：
  - 最大报文段长度`MSS`选项
  - 窗口扩大选项
  - 时间戳选项
  - 选择确认选项
- **填充**：由于选项的长度可变，因此使用填充来**确保报文段首部能被4整除**（因为数据偏移字段，也就是首部长度字段，是以4字节为单位的）。

# 应用层

## 概述

应用层是计算机网络体系结构的**最顶层**，是**设计和建立计算机网络的最终目的**，也是计算机网络中发展最快的部分。

## 客户/服务器方式（C / S）和对等方式（P2P）

**客户/服务器（Client/Server）方式**

- 客户和服务器是指通信中所设计的两个应用进程。
- 客户/服务器方式所描述的是进程之间服务和被服务的关系。
- 客户是服务请求方，服务器是服务提供方。
- 服务器总是处于运行状态，并等待客户的服务请求。服务器具有固定端口号（例如`HTTP`服务器的默认端口号为80），而运行服务器的主机也具有固定的`IP`地址。

**对等（Peer-to-Peer）方式**

- 再`P2P`方式中，**没有固定的服务请求者和服务提供者**，分布在网络边缘各端系统中的应用进程是对等的，被称为**对等方**。**对等方相互之间直接通信**，每个对等方既是服务的请求者，又是服务的提供者。
- 目前流行的`P2P`应用主要包括`P2P`文件共享、即时通信、`P2P`流媒体、分布式存储等。
- 基于`P2P`的应用是**服务分散型**的。
- `P2P`方式的最突出特性之一就是它的**可扩展性**。因为每增加一个对等方，不仅增加了服务请求者，也增加了提供者，系统性能不会因规模的增大而降低。

## 动态主机配置协议 DHCP

- 动态主机配置协议`DHCP(Dynamic Host Configuration Protocol)`提供了一种机制，称为即插即用连网。这种机制**允许一台计算机加入新网络时可自动获取`IP`地址等网络配置信息而不用手工参与**。
- `DHCP`报文**在运输层使用`UDP`协议封装**。
- `DHCP`客户在未获取到`IP`地址时使用地址`0.0.0.0`。
- 在每一个网络上都设置一个`DHCP`服务器会使`DHCP`服务器的数量太多。因此现在是使每一个网络至少有一个`DHCP`中继代理（通常是一台路由器），它配置了`DHCP`服务器的`IP`地址信息，作为各网络中计算机与`DHCP`服务器的桥梁。

![DHCP的作用](ComputerNetwork/20211112211406.png)

## 域名系统 DNS

- 因特网采用**层次树状结构的域名结构**。
- 域名的结构由若干个分量组成，各分量之间用“点”隔开，分别代表不同级别的域名。
  - 每一级的域名都由英文字母和数字组成，不超过63个字符，不区分大小写字母
  - 级别最低的域名写在最左边，而级别最高的顶级域名写在最右边
  - 完整的域名不超过255个字符

顶级域名`TLD(Top Level Domain)`分为三类：

- 国家顶级域名`nTLD`

  如`cn`、`us`、`uk`等。

- 通用顶级域名`gTLD`

  最常见的7个：`com`、`net` 、`org`、`int`、`edu`、`gov`、`mil`。

- 反向域`arpa`

  用于反向域名解析，即`IP`地址反向解析为域名。

![域名空间](ComputerNetwork/20211112213954.png)

域名和IP地址的映射关系必须保存在域名服务器中，供所有其他应用查询。显然不能将所有信息都储存在一台域名服务器中。DNS使用**分布在各地的域名服务器**来实现域名到IP地址的转换。

域名服务器可以划分为以下四种不同的类型：

- **根域名服务器**

  根域名服务器通常并不直接对域名进行解析，而是返回该域名所属顶级域名的顶级域名服务器的`IP`地址。

- **顶级域名服务器**

  管理在该顶级域名服务器注册的所有二级域名。

- **权限域名服务器**

  管理某个区的域名。

- **本地域名服务器**

  本地域名服务器起着代理的作用，会将该报文转发到上述的域名服务器的等级结构中。

域名解析过程有**递归查询**和**迭代查询**。

![递归查询](ComputerNetwork/20211112214558.png)

![递归 + 迭代查询（常用）](ComputerNetwork/20211112214621.png)

为了提高DNS的查询效率，并减轻根域名服务器的负荷和减少因特网上的DNS查询报文数量，在域名服务器中广泛地使用了**高速缓存**。高速缓存用来存放最近查询过的域名以及从何处获得域名映射信息的记录。

由于域名到IP地址的映射关系并不是永久不变，为保持高速缓存中的内容正确，域名服务器**应为每项内容设置计时器并删除超过合理时间的项**（例如，每个项目只存放两天）。

不但在本地域名服务器中需要高速缓存，在用户主机中也很需要。

`DNS`报文使用运输层的`UDP`协议进行封装，运输层**端口号为53**。

## 文件传送协议 FTP

文件传送协议`FTP(File Transfer Protocol)`是因特网上使用的最广泛的文件传送协议。

- `FTP`**提供交互式的访问**，允许客户**指明文件的类型与格式**（如指明是否使用`ASCII`码），并允许文件具有存取权限（如访问文件的用户必须经过授权）。
- `FTP`屏蔽了各计算机系统的细节，因而适合在异构网络中任意计算机之间传送文件。

![主动模式与被动模式](ComputerNetwork/20211112215837.png)

## 电子邮件

电子邮件发送过程：

1. 发件人将邮件发送到自己的**邮件服务器**
2. 邮件服务器按1其目的地址转发
3. 收件人随时可获取收到的电子邮件

电子邮件系统采用 C/S 方式，有3个主要组成构件：用户代理，邮件服务器以及电子邮件所需要的协议。

- **用户代理**是用户与电子邮件系统的接口，又称为**电子邮件客户端软件**。
- **邮件服务器**是电子邮件系统的基础设施，其功能是**发送和接收邮件**，同时还要负责维护用户的邮箱。
- 协议包括邮件发送协议（例如`SMTP`）和邮件读取协议（例如`POP3`，`IMAP`）。

![邮件发送过程](ComputerNetwork/20211112220644.png)

`SMTP(Simple Mail Transfer Protocol)`协议只能传送`ASCII`码文本数据，不能传送可执行文件或其他的二进制对象。不能满足传送多媒体邮件的需要，为解决`SMTP`传送非`ASCII`码文本的问题，提出了多用途因特网邮件扩展`MIME(Multipurpose Internet MailExtensions)`。

## 万维网 WWW

万维网`WWW(World Wide Web)`**并非某种特殊的计算机网络**。它是一个大规模的、联机式的信息储藏所，**是运行在因特网上的一个分布式应用**。

- 万维网利用网页之间的**超链接**将不同网站的网页链接成一张逻辑上的信息网。

- 万维网使用**统一资源定位符`URL`**来指明因特网上任何种类“资源”的位置。
- `URL`的一般形式由以下四个部分组成：`<协议>://<主机>:<端口>/<路径>`

**超文本传输协议`HTTP(HyperText Transfer Protocol)`**

`HTTP`定义了浏览器怎样向万维网服务器请求万维网文档，以及万维网服务器怎样把万维网文档传送给浏览器。

- `HTTP/1.0`采用**非持续连接**方式。在该方式下，每次浏览器要请求一个文件都要与服务器建立`TCP`连接，当收到响应后就立即关闭连接。

  - **每请求一个文档就要有两倍的`RTT`的开销**。若一个网页上有很多引用对象（例如图片等)，那么请求每一个对象都需要花费`2RTT`	的时间。
  - 为了减小时延，**浏览器通常会建立多个并行的`TCP`连接同时请求多个对象**。但是，这会大量占用万维网服务器的资源，特别是万维网服务器往往要同时服务于大量客户的请求，这会使其负担很重。

  ![请求文档过程](ComputerNetwork/20211113094310.png)

- `HTTP/1.1`采用**持续连接**方式。在该方式下，万维网服务器在发送响应后仍然保持这条连接，使同一个客户（浏览器）和该服务器可以继续在这条连接上传送后续的`HTTP`请求报文和响应报文。这并不局限于传送同一个页面上引用的对象，而是只要这些文档都在同一个服务器上就行。

  - 为了进一步提高效率，`HTTP/1.1`的持续连接还可以使用**流水线**方式工作，即浏览器在收到HTTP的响应报文之前就能够连续发送多个请求报文。

`HTTP`的报文格式

`HTTP`是**面向文本**的，其报文中的每一个**字段**都是一些**`ASCII`码串**，并且每个字段的**长度**都是**不确定**的。

![HTTP请求报文格式](ComputerNetwork/20211113094654.png)

![HTTP响应报文格式](ComputerNetwork/20211113094744.png)

`Cookie`是一种对无状态的`HTTP`进行状态化的技术，使得万维网服务器能够记住用户。

![Cookie原理](ComputerNetwork/20211113095102.png)

万维网缓存与代理服务器

- 利用缓存机制可以提高万维网效率
- 万维网缓存又称为`Web缓存(Web Cache)`，可位于客户机，也可位于中间系统上，位于中间系统上的`Web`缓存又称为**代理服务器**`(Proxy Server)`。
- `Web`缓存把最近的一些请求和响应暂存在本地磁盘中。当新请求到达时，若发现这个请求与暂时存放的请求相同，就返回暂存的响应，而不需要按`URL`的地址再次去因特网访问资源。

# 参考

1. [计算机网络微课堂-湖科大教书匠](https://www.bilibili.com/video/BV1c4411d7jb)