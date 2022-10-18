# `简介`

**本篇博客是对 湖南科技大学-高军-计算机网络 课程笔记记录，具体请移步课程[计算机网络](https://www.xueyinonline.com/detail/222640205)**

# `概述`

## `因特网`

**01.网络：若干节点和连接结点的链路形成的集合**

**02.互联网：多个网络通过路由器互联形成互联网**

**03.因特网：世界上最大的互联网**

**04.ISP：Internet Service Provide 因特网服务提供商（中国移动、联通等）**

## `信息交换(3种)`

**01.电路交换**

**📞——用户线——（电话交换机——中继线——电话交换机）n——用户线——📞**

**02.报文交换**

**发送方A——B——C——接受方D**

**03.分组交换**

**信息等分添加首部——分多个路由线路缓存转发——去除首部，信息合并**

**对比如下：**

![](https://pic.imgdb.cn/item/621c88be2ab3f51d9164db82.jpg)

## `计算机网络的定义`

![](https://pic.imgdb.cn/item/621c893a2ab3f51d9165dcf4.jpg)

## `计算机网络的分类`

![](https://pic.imgdb.cn/item/621c897a2ab3f51d91665597.jpg)

## `网络性能指标`

### `比特`

**以下为数据量单位**

| 1B | 8bit |
| :--: | :--: |
|   1KB   |  2 ^ 10 B   |
| 1MB  |   2 ^ 20 B   |
|  1GB    |   2 ^ 30 B   |
| 1TB | 2 ^ 40 B |

**拓展：买来的固态硬盘和系统上显示的大小不一样的原因是厂家使用的数据量单位和计算机的不一样，厂家的1GB = 10 ^ 9 B ，换算成计算机显示的大小应该将总的 Byte /  2 ^ 20**

### `速率`

**以下为数据传送时比特率或数据率单位**

**bit/s（b/s、bps）**

| bit/s |  b/s、bps   |
| :---: | :---------: |
| Kbps  | 10 ^ 3 bps  |
| Mbps  | 10 ^ 6 bps  |
| Gbps  | 10 ^ 9 bps  |
| Tbps  | 10 ^ 12 bps |

![](https://pic.imgdb.cn/item/621c8d9c2ab3f51d916decbc.jpg)

### `带宽`

**两种表述：**

![](https://pic.imgdb.cn/item/621c8de52ab3f51d916e6c91.jpg)

### `吞吐量`

![](https://pic.imgdb.cn/item/621c8e212ab3f51d916ec85a.jpg)

### `时延`

**01.三种时延**

![](https://pic.imgdb.cn/item/621c8e4d2ab3f51d916f0ab0.jpg)

**02.如何计算？**

![](https://pic.imgdb.cn/item/621c8fa42ab3f51d91719819.jpg)

**03.例题**

![](https://pic.imgdb.cn/item/621c90642ab3f51d9173d036.jpg)

### `时延带宽积`

![](https://pic.imgdb.cn/item/621c93cc2ab3f51d9179858f.jpg)

### `往返时间`

![](https://pic.imgdb.cn/item/621c945e2ab3f51d917aabc2.jpg)

### `利用率`

![](https://pic.imgdb.cn/item/621c95172ab3f51d917bf16a.jpg)

### `丢包率`

![](https://pic.imgdb.cn/item/621c95e22ab3f51d917d2a16.jpg)

## `计算机网络体系结构`

**01.OSI：法律上的国际标准、7层**
**02. TCP/IP：事实上的国际标准、4层**

![图片1](https://pic.imgdb.cn/item/623075485baa1a80ab6b9fff.jpg)

**03.原理体系结构：因为TCP/IP体系网络接口层的不确定，事实上TCP/IP只有3层，学习时为了补上这缺失的一环，我们综合OSI体系和TCP/IP体系成为原理体系结构，将TCP/IP中的网络接口层替换为物理层+数据链路层、5层**

![图片2](https://pic.imgdb.cn/item/623075625baa1a80ab6ba893.jpg)

## `分层的必要性`

**01. Ａ—— B两台主机连接，如何让传输信息：接口，线路，传输比特流的物理方式 —— 物理层**
**02. 多台主机的主线网络中，如何正确接收比特流，标识主机地址，MAC，协调主机争用主线 —— 数据链路层（主线网络已经弃用，现如今使用的是交换机网络）**
**03.多个网络通过路由器互联，如何标识不同的网络和网络中的多个主机，IP地址，如何路由转发分组 —— 网络层**
**04. 不同主机间的两个进程相互通信，如何正确接受信号，传输错误时如何处理？—— 运输层**
**05.不同类型网络应用程序之间相互通信，邮件SMTP，万维网应用HTTP，文件传输FTP —— 应用层**

![图片](https://pic.imgdb.cn/item/623075805baa1a80ab6bb34b.jpg)

## `网络体系结构分层思想举例`

**例子：浏览器 —— web服务器**
**应用层（HTTP）—— 运输层（HTTP+TCP）—— 网络层（HTTP+TCP+IP）—— 数据链路层（帧 ETH+HTTP+TCP+IP+ETH）—— 物理层（前导码+ETH+HTTP+TCP+IP+ETH）—— 比特流—— 路由器 —— （物理层 、链路层、网络层、网络层、链路层、物理层 ）—— web服务器 （相反过程）**

## `专用术语`

### `实体`

![](https://pic.imgdb.cn/item/623078525baa1a80ab6cccea.jpg)

### `协议`

**逻辑通信协议实际上并不存在，只是为了在考虑某一层通讯时，更能具体描述**

![](https://pic.imgdb.cn/item/623078c35baa1a80ab6cfdb6.jpg)





### `服务`

![](https://pic.imgdb.cn/item/623079f15baa1a80ab6da392.jpg)

**Note：下面的协议对上面的实体是透明的，实体看得见相邻下层所提供的服务，但不知道服务的具体协议，相对而言是透明的**

![](https://pic.imgdb.cn/item/62307d585baa1a80ab6ef024.jpg)

![](https://pic.imgdb.cn/item/62307d855baa1a80ab6efcfc.jpg)

# `物理层`

## `基本概念`

**Note：物理层就是为了解决在不同的传输媒体上传输比特流的问题，进而给数据链路层提供透明传输比特流的服务，数据链路层不能看见，也无需看见物理层是如何传输比特流的，只需要享受物理层带来的服务即可。**

### `传输媒体的类型`

**01.导引型：双绞线、同轴电缆、光纤**
**02.非导引型：微波通信（2-40Hz）**

### `物理层协议的主要任务`

**01.机械特性：指明接口的形状、尺寸、引脚数目等**
**02.电气特性：指明接口电缆上的电压范围，电缆长度**
**03.功能特性：指明不同电压代表什么意义**
**04.过程特性：指明对于不同功能的各自可能事件的出现顺序**

## `物理层下的传输媒体`

**Note：传输媒体严格意义上不属于任何一个层次，只能算在物理层之下，本节了解即可**

![](https://pic.imgdb.cn/item/6231d7695baa1a80ab2ffa2b.jpg)

### `导引型`

**含义：电磁波被导引沿着固体媒体传播**
**例子：同轴电缆、双绞线、光纤、电力线**

**01.同轴电缆**

![图片123…](https://pic.imgdb.cn/item/6231d62b5baa1a80ab2d760d.jpg)

**02.双绞线**

![](https://pic.imgdb.cn/item/6231d6675baa1a80ab2de6ea.jpg)

**03.光纤**

![](https://pic.imgdb.cn/item/6231d69a5baa1a80ab2e4bec.jpg)

**04.电力线**

![](https://pic.imgdb.cn/item/6231d6b25baa1a80ab2e7a40.jpg)

### `非导引型`

**含义：自由空间**
**例子：无线电波、微波、红外线、可见光**

![](https://pic.imgdb.cn/item/6231d6ce5baa1a80ab2eb13b.jpg)

**01.无线电波**

![](https://pic.imgdb.cn/item/6231d6ff5baa1a80ab2f1c3c.jpg)

**02.微波**

![](https://pic.imgdb.cn/item/6231d7175baa1a80ab2f5025.jpg)

**03.红外线**

![](https://pic.imgdb.cn/item/6231d7305baa1a80ab2f8395.jpg)

**04.可见光**

**LIFI（Light Fidelity）光保真技术，又称为可见光无线通信，该技术是一种利用可见光波谱进行数据传输的全新无线传输技术。LIFI通过在LED上植入一个微小的芯片，利用电信号控制[发光二极管](https://baike.baidu.com/item/发光二极管/1521336)（LED）发出肉眼看不到的高速闪烁信号来传输信息，这种技术做成的系统能够覆盖室内灯光达到的范围，电脑不需要电线连接只要在室内开启电灯，无需WIFI也可接入互联网。**


## `传输方式`

### `串行传输与并行`

![](https://pic.imgdb.cn/item/6231d7b65baa1a80ab309d6f.jpg)

### `同步与异步`

![](https://pic.imgdb.cn/item/6231d7d95baa1a80ab30e036.jpg)

### `单工、半双工和全双工`

![](https://pic.imgdb.cn/item/6231d81c5baa1a80ab316358.jpg)



**例题：**
一次传输一个字符（5~8位组成），每个字符用一个起始码引导，同一个停止码结束，如果没有数据发送，发送方可以连续发送停止码，这种通信方式称为

A.并行传输
B.串行传输
C.同步传输
D.异步传输

**解析：每个字符（5~8位组成）为一段，需要连续发生停止码，不同步 —— 异步通讯**

## `编码与调制`
### `为何需要编码与调制 ？`
**一、文字、图片、视频 （消息）—— 比特流（数据）—— 信号（物理电磁表现）—— 基带信号（信号源发出的原始信号） **
**二、为了让基带信号顺利在数字信号 or 模拟信号中传播，我们需要对其进行编码 or 调制**

![](https://pic.imgdb.cn/item/625d478b239250f7c5546df3.jpg)

### `传输媒体与信道的关系`

**01.对于单工传输：传输媒体中只包含一条发送 / 接收信道**
**02.对于双工传输：传输媒体中包含一条发送和一条接收信道**
**03.若使用信道复用技术，传输媒体中可以同时包含多条信道**

### `编码`

![](https://pic.imgdb.cn/item/625d4814239250f7c555e946.jpg)

**编码练习题：**

![](https://pic.imgdb.cn/item/625d487f239250f7c55722ff.jpg)

`调制`

![](https://pic.imgdb.cn/item/625d48ac239250f7c557aa06.jpg)

### `混合调制`

**频率相位振幅间的关系**

<img src="https://pic.imgdb.cn/item/625d48d5239250f7c55815b4.jpg" style="zoom:50%;" />

**QAM - 16**

![](https://pic.imgdb.cn/item/625d4902239250f7c5589e1e.jpg)

## `信道的极限容量`

### `失真`

![](https://pic.imgdb.cn/item/625d49d6239250f7c55ae298.jpg)

### `奈氏准则`
![](https://pic.imgdb.cn/item/625d4a2f239250f7c55bce64.jpg)

### `香农公式`


![](https://pic.imgdb.cn/item/625d4a50239250f7c55c2bfd.jpg)

### `综合来看奈和香`

![](https://pic.imgdb.cn/item/625d4a76239250f7c55c962a.jpg)

### `例题`

![](https://pic.imgdb.cn/item/625d4a9d239250f7c55d0079.jpg)

![](https://pic.imgdb.cn/item/625d4af8239250f7c55df507.jpg)

![](https://pic.imgdb.cn/item/625d4b12239250f7c55e3697.jpg)

 # `数据链路层`
## `概述`
**一、主机之间通讯时，我们可以暂时忽略除了数据链路层之外的其他层的交互，看成各个链路之间的信息交互**

![2：56](https://pic.imgdb.cn/item/6265328a239250f7c5b6704c.jpg)

**二、数据链路层的三个重要问题**
**01.封装成帧**
**对来自网络层的协议数据包添加帧头和帧尾成为封装成帧**
**02.差错检测**
**接收方检查帧尾的检错码来判断是否出错**
**03.可靠传输**
**发送方发送什么，接收方就能收到什么，期间可能有backup**

**三、使用广播信道的数据链路层**

**01.帧需要包含地址**
**02.CSMA/CD来防止碰撞💥**

## `封装成帧`
![](https://pic.imgdb.cn/item/6265334c239250f7c5b89e29.jpg)

**例题：**
![](https://pic.imgdb.cn/item/62653372239250f7c5b90aec.jpg)

**MTU**

![](https://pic.imgdb.cn/item/626532d0239250f7c5b7268a.jpg)

## `差错检测`
![](https://pic.imgdb.cn/item/626533b4239250f7c5b9c16e.jpg)

**一、奇偶校验**

![](https://pic.imgdb.cn/item/626533db239250f7c5ba258c.jpg)

**二、循环冗余校验**

![](https://pic.imgdb.cn/item/62653416239250f7c5bac53e.jpg)

**二进制除法有两种，一是常规除法、二是模2除法**

**模2除法位数相等异或即可，不够则补零**

**例题：**
![](https://pic.imgdb.cn/item/62653444239250f7c5bb41ab.jpg)
![](https://pic.imgdb.cn/item/6265346b239250f7c5bba7e3.jpg)

**总结**
![](https://pic.imgdb.cn/item/6265349c239250f7c5bc2ba6.jpg)

## `可靠传输`

### `可靠传输的基本概念`

![](https://pic.imgdb.cn/item/6266542f239250f7c51a86ef.jpg)

![](https://pic.imgdb.cn/item/626654e1239250f7c51c0c07.jpg)

### `停止-等待协议`

![](https://pic.imgdb.cn/item/626661ae239250f7c539d593.jpg)

**Note：**

![](https://pic.imgdb.cn/item/62665824239250f7c52376a4.jpg)

**SW协议的信道利用率**

![](https://pic.imgdb.cn/item/626659de239250f7c5276a69.jpg)

**例题：**

![](https://pic.imgdb.cn/item/62665b7b239250f7c52b25ec.jpg)

### `回退N帧协议`

**发送方连续发送多个分组，接收方一个个接受，可以选择累积确认，当出现差错时需要回退若干帧重发**

![](https://pic.imgdb.cn/item/626667cd239250f7c547b19d.jpg)

**有误码的情况**

![](https://pic.imgdb.cn/item/6266689c239250f7c5498100.jpg)

![](https://pic.imgdb.cn/item/626668d8239250f7c54a0f45.jpg)

**Summary：**

![](https://pic.imgdb.cn/item/626669fe239250f7c54caf77.jpg)

**例题：**

![](https://pic.imgdb.cn/item/62666adf239250f7c54ec966.jpg)

### `选择重传协议`

**发送方面和接受方均为一个窗口。每个窗口内部所有数据处理完才能向下滑动，发送方`选择`窗口内`未确认`的分组`重`发给接收方，故名为`选择重传协议`**

![](https://pic.imgdb.cn/item/6268dd4d239250f7c562bdd7.jpg)

![](https://pic.imgdb.cn/item/6268dd4d239250f7c562bddf.jpg)

**窗口尺寸**

![](https://pic.imgdb.cn/item/6268dd4d239250f7c562bdf6.jpg)

**尺寸超限的后果**

![](https://pic.imgdb.cn/item/6268dd4d239250f7c562be08.jpg)

**Summary**

![](https://pic.imgdb.cn/item/6268dd4d239250f7c562be13.jpg)

**例题：**

![](https://pic.imgdb.cn/item/6268dde6239250f7c5634c33.jpg) 

## `点对点协议PPP`

### `概述`

![](https://pic.imgdb.cn/item/626dcf4b239250f7c539b0f8.jpg)

![](https://pic.imgdb.cn/item/626dcf98239250f7c53a1a54.jpg)

### `PPP帧`

![](https://pic.imgdb.cn/item/626dd046239250f7c53b0eab.png)

### `透明传输`

![](https://pic.imgdb.cn/item/626dd06b239250f7c53b4ae3.png)

![](https://pic.imgdb.cn/item/626dd06b239250f7c53b4ae6.png)

### `差错检验`

![](https://pic.imgdb.cn/item/626dd094239250f7c53b85c1.png)

### `工作状态`

![](https://pic.imgdb.cn/item/626dd094239250f7c53b85c4.png)

## `媒体接入控制MAC`

### `基本概念`

![](https://pic.imgdb.cn/item/626dd758239250f7c545ec6e.jpg)

**Note：**

![](https://pic.imgdb.cn/item/626dd76f239250f7c54614ff.jpg)

### `静态划分信道`

**一、什么是信道复用？**

![](https://pic.imgdb.cn/item/626e251c239250f7c5f5ab32.jpg)

**二、四种复用技术**

**01.FDM**

![](https://pic.imgdb.cn/item/626e25f9239250f7c5f7ceac.jpg)

**02.TDM**

![](https://pic.imgdb.cn/item/626e265e239250f7c5f8db91.jpg)

**03.WDM**

![](https://pic.imgdb.cn/item/626e26ba239250f7c5f9b4cc.jpg)

**04.CDM**

![](https://pic.imgdb.cn/item/626e272f239250f7c5facccf.jpg)

![](https://pic.imgdb.cn/item/626e283a239250f7c5fd39f1.jpg)

**例子：**

![](https://pic.imgdb.cn/item/626e28c2239250f7c5fe7c5d.jpg)

**Note：严格的要求正交是为了方便后续判断站点是否发送信号**

**例题：**

![](https://pic.imgdb.cn/item/626e2a0a239250f7c501bcdc.jpg)

![](https://pic.imgdb.cn/item/626e2b27239250f7c5047eb7.jpg)

### `动态接入控制 `

#### `CSMA/CD`

**一、概述**

![](https://pic.imgdb.cn/item/626e2d95239250f7c50a6609.jpg)

**二、例子：**

![](https://pic.imgdb.cn/item/626e3166239250f7c513c2dc.jpg)

**三、CSMA/CD 的争用期**

![](https://pic.imgdb.cn/item/626e326c239250f7c51623c3.jpg)

**四、CSMA/CD的最小/大帧长**

**最小帧长 = 数据传输率 x RTT**

![](https://pic.imgdb.cn/item/626e32f9239250f7c51777fa.jpg)

![](https://pic.imgdb.cn/item/626e33df239250f7c5198b95.jpg)

**五、退避时间**

![](https://pic.imgdb.cn/item/626e350c239250f7c51c8786.jpg)	

**六、信道利用率**

![](https://pic.imgdb.cn/item/626e3595239250f7c51dcfa3.jpg)

**七、帧发送/接收流程**

![](https://pic.imgdb.cn/item/626e35d9239250f7c51e7bab.jpg)

![](https://pic.imgdb.cn/item/626e362c239250f7c51f4718.jpg)

**例题：**

![](https://pic.imgdb.cn/item/626e36ba239250f7c520a893.jpg)

![](https://pic.imgdb.cn/item/626e3766239250f7c5225be0.jpg)

![](https://pic.imgdb.cn/item/626e3805239250f7c523eeaf.jpg)

![](https://pic.imgdb.cn/item/626e3819239250f7c5241a7e.jpg)

**Summary：**

![](https://pic.imgdb.cn/item/626e385b239250f7c524ba33.jpg)

#### `CSMA/CA `

**略**

## `MAC地址，IP地址及ARP协议`

### `MAC地址`

**一、引入**

**01.使用点对点信道不需要使用地址，因为接收方是固定的**

**02.如果使用广播信道**

![](https://pic.imgdb.cn/item/6281babe0947543129ad1b5a.jpg)

**二、概述**

![](https://pic.imgdb.cn/item/6281baf90947543129adb5e8.jpg)

![](https://pic.imgdb.cn/item/6281bb490947543129ae7b95.jpg)

**例题：**

![](https://pic.imgdb.cn/item/6281bb680947543129aec58c.jpg)

![](https://pic.imgdb.cn/item/6281bb8d0947543129af2506.jpg)

**三、MAC地址格式**

![](https://pic.imgdb.cn/item/6281bbb70947543129af90b1.jpg)

![](https://pic.imgdb.cn/item/6281be450947543129b63360.jpg)

**四、发送顺序**

![](https://pic.imgdb.cn/item/6281be780947543129b6b0c5.jpg)

**五、例子**

![](https://pic.imgdb.cn/item/6281be9e0947543129b70969.jpg)

![](https://pic.imgdb.cn/item/6281bebc0947543129b74e80.jpg)

![](https://pic.imgdb.cn/item/6281bf010947543129b801aa.jpg)

**随机MAC地址**

![](https://pic.imgdb.cn/item/6281bf2d0947543129b89996.jpg)

### `IP地址`

**一、概述**

![](https://pic.imgdb.cn/item/6281c8b00947543129d2249c.jpg)

**二、从网络体系结构看IP和MAC地址**

![](https://pic.imgdb.cn/item/6281c8f10947543129d2d656.jpg)

**三、IP和MAC变化情况**

![](https://pic.imgdb.cn/item/6281c9200947543129d34f33.jpg)

![](https://pic.imgdb.cn/item/6281c94f0947543129d3c4e9.jpg)

### `ARP协议`

**目的：为了知道IP地址对应的MAC地址是什么**

**第一步：发送广播型ARP请求报文**

![](https://pic.imgdb.cn/item/6281d7810947543129ff47cc.jpg)

**第二步：接收IP和MAC信息**

![](https://pic.imgdb.cn/item/6281d7b70947543129ffee81.jpg)

**第三步：添加IP和MAC信息到ARP高速缓存中**

![](https://pic.imgdb.cn/item/6281d7d909475431290059ac.jpg)

**高速缓存记录属性**

![](https://pic.imgdb.cn/item/6281d84c094754312901cd60.jpg)

**另外ARP协议只能在同一个链路使用，如下图：**

![](https://pic.imgdb.cn/item/6281d8880947543129027f8e.jpg)

## `集线器和交换机的区别`

**一、集线器**

**集线器取代了早期同轴电缆连接的总线**

![](https://pic.imgdb.cn/item/62837b2d094754312921f5b2.jpg)

**使用集线器在物理层拓展以太网**

![](https://pic.imgdb.cn/item/62837bc8094754312924150d.jpg)

![](https://pic.imgdb.cn/item/62837bdf09475431292463f9.jpg)

**二、交换机**

![](https://pic.imgdb.cn/item/62837c04094754312924e0d8.jpg)

![](https://pic.imgdb.cn/item/62837c250947543129254d95.jpg)

**三、二者区别**

![](https://pic.imgdb.cn/item/62837c50094754312925ded0.jpg)

![](https://pic.imgdb.cn/item/62837c74094754312926593a.jpg)

## `以太网交换机自学习和转发帧的流程`

## `以太网交换机的生成树协议STP`

## `虚拟局域网VLAN`

# `网络层`

## `网络层概述`

### `任务`

**网络层的主要任务是实现各网络之间的互联，既然实现数据包在各个网络之间的传输**

![](https://pic.imgdb.cn/item/62837ffb09475431293294f5.jpg)

### `需要解决的问题`
- **网络成向运输层提供的是可靠传输服务还是不可靠传输服务**

- **网络寻址问题**

  ![](https://pic.imgdb.cn/item/628380bb094754312934fd1c.jpg)

- **路由选择问题**

  ![](https://pic.imgdb.cn/item/628380d60947543129355236.jpg)

### `总结`

![](https://pic.imgdb.cn/item/628381150947543129361b22.jpg)

## `网络层提供的两种服务`

### `面向连接的虚电路服务`

![](https://pic.imgdb.cn/item/62839bb70947543129a2fa68.jpg)

### `无连接的数据报服务`

![](https://pic.imgdb.cn/item/62839be10947543129a3c8f5.jpg)

### `两种服务比较`

![](https://pic.imgdb.cn/item/62839c1f0947543129a4f900.jpg)

