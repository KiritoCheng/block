<div class="rich_media_content " id="js_content" style="visibility: visible;"><section data-mpa-powered-by="yiban.io">> 这一篇主要和大家一起学习回顾关于&nbsp;**TCP/IP**&nbsp;的常见攻击，至少有一个基本的认识。

## <span style="font-size: inherit;color: inherit;line-height: inherit;">前言</span>
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIw6BQa4k59ZoKHN1qVzfCj37eMgk30wJoI9gYHicALeBJEr2Xvf3xsgEA/640?wx_fmt=png "在这里插入图片描述")<figcaption style="line-height: inherit;margin-top: 10px;text-align: center;color: rgb(153, 153, 153);font-size: 0.7em;">前言
</figcaption></figure>

## <span style="font-size: inherit;color: inherit;line-height: inherit;">1 IP欺骗</span>
> IP是什么？

在网络中，所有的设备都会分配一个地址。这个地址就仿佛小蓝的家地址「**多少号多少室**」，这个号就是分配给整个子网的，「**室**」对应的号码即分配给子网中计算机的，这就是网络中的地址。「号」对应的号码为网络号，「**室**」对应的号码为主机号，这个地址的整体就是**IP地址**。
> 通过IP地址我们能知道什么？

通过 IP 地址，我们就可以判断访问对象服务器的位置，从而将消息发送到服务器。一般发送者发出的消息首先经过子网的集线器，转发到最近的路由器，然后根据路由位置访问下一个路由器的位置，直到终点。
> IP头部格式<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwoRsXoRq5q3nxJO0epRTGbFWfzjurvqJfECS0QugIHs6AYFkn3DJkbw/640?wx_fmt=png "IP头部格式")<figcaption style="line-height: inherit;margin-top: 10px;text-align: center;color: rgb(153, 153, 153);font-size: 0.7em;">IP头部格式</figcaption></figure>> IP欺骗技术

骗呗，拐骗，诱骗！

IP 欺骗技术就是**伪造**某台主机的 IP 地址的技术。通过 IP 地址的伪装使得某台主机能够**伪装**另外的一台主机，而这台主机往往具有某种特权或者被另外的主机所信任。

假设现在有一个合法用户 **(1.1.1.1)** 已经同服务器建立正常的连接，攻击者构造攻击的 TCP 数据，伪装自己的 IP 为 **1.1.1.1**，并向服务器发送一个带有 RSI 位的 TCP 数据段。服务器接收到这样的数据后，认为从 **1.1.1.1** 发送的连接有错误，就会清空缓冲区中建立好的连接。

这时，如果合法用户 **1.1.1.1** 再发送合法数据，服务器就已经没有这样的连接了，该用户就必须重新开始建立连接。攻击时，伪造大量的IP地址，向目标发送 RST 数据，使服务器不对合法用户服务。虽然IP地址欺骗攻击有着相当难度，但我们应该清醒地意识到，这种攻击非常广泛，入侵往往从这种攻击开始。

## <span style="font-size: inherit;color: inherit;line-height: inherit;">2 SYN Flooding</span>
> SYN Flooding 简介

拒绝服务攻击（DDoS）从 1970 年出现直到今天都依然在作祟，并给全球范围内的各大组织带来了不可估量的损失。**SYN Flood&nbsp;**是互联网上最经典的 DDoS 攻击方式之一，最早出现于 1999 年左右，雅虎是当时最著名的受害者。**SYN Flood&nbsp;**攻击利用了 **TCP** 三次握手的缺陷，能够以较小代价使目标服务器无法响应，且难以追查。

**SYN&nbsp;flood** 是一种常见的 **DOS**（denial of service拒绝服务）和 **DDos** (distributed denial of serivce 分布式拒绝服务）攻击方式。这是一种使用 TCP 协议缺陷，发送大量的**伪造的 TCP 连接请求**，使得被攻击方 CPU 或内存资源耗尽，最终导致被攻击方无法提供正常的服务。
> TCP SYN Flood 攻击原理

**TCP&nbsp;SYN Flood** 攻击利用的是 **TCP** 的三次握手（**SYN -&gt; SYN/ACK -&gt; ACK**），假设连接发起方是A，连接接受方是 B，即 B 在某个端口（**Port**）上监听 A 发出的连接请求，过程如下图所示，左边是 A，右边是 B。
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwgqYz9sHCvK9I6K6dfyibJfRdauAMpvHoDl0vM3RsvsXNOtnnXABrFuA/640?wx_fmt=png "在这里插入图片描述")</figure>

A 首先发送 **SYN**（Synchronization）消息给 B，要求 B 做好接收数据的准备；B 收到后反馈 **SYN-ACK**（Synchronization-Acknowledgement） 消息给 A，这个消息的目的有两个：

*   向 A 确认已做好接收数据的准备。

*   同时要求 A 也做好接收数据的准备，此时 B 已向 A 确认好接收状态，并等待 A 的确认，连接处于**半开状态（Half-Open）**，顾名思义只开了一半；A 收到后再次发送 **ACK** (Acknowledgement) 消息给 B，向 B 确认也做好了接收数据的准备，至此三次握手完成，「**连接**」就建立了。

大家注意到没有，最关键的一点在于双方是否都按对方的要求进入了**可以接收消息**的状态。而这个状态的确认主要是双方将要使用的**消息序号(**SquenceNum)，**TCP** 为保证消息按发送顺序抵达接收方的上层应用，需要用**消息序号**来标记消息的发送先后顺序的。

**TCP&nbsp;**是「**双工**」(Duplex)连接，同时支持双向通信，也就是双方同时可向对方发送消息，其中 **SYN** 和 **SYN-ACK** 消息开启了 A→B 的单向通信通道（B 获知了 A 的消息序号）；**SYN-ACK** 和 **ACK** 消息开启了 B→A 单向通信通道（A 获知了 B 的消息序号）。

上面讨论的是双方在诚实守信，正常情况下的通信。

但实际情况是，网络可能不稳定会丢包，使握手消息不能抵达对方，也可能是对方故意不按规矩来，故意延迟或不发送握手确认消息。

假设&nbsp;B 通过某 **TCP** 端口提供服务，B 在收到 A 的 **SYN** 消息时，积极地反馈了 **SYN-ACK** 消息，使连接进入**半开状态**，因为 B 不确定自己发给 A 的 **SYN-ACK** 消息或 A 反馈的 ACK 消息是否会丢在半路，所以会给每个待完成的半开连接都设一个&nbsp;**Timer**，如果超过时间还没有收到 A 的 **ACK** 消息，则重新发送一次 **SYN-ACK** 消息给 A，直到重试超过一定次数时才会放弃。
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwX7L1SmkpPysDtuHJFGwTfS2zHzs3iaTnf8oI8AmW41j5YyaXPs7VzcQ/640?wx_fmt=png)</figure>

B 为帮助 A 能顺利连接，需要**分配内核资源**维护半开连接，那么当 B 面临海量的连接 A 时，如上图所示，**SYN Flood** 攻击就形成了。攻击方 A 可以控制肉鸡向 B 发送大量 SYN 消息但不响应 ACK 消息，或者干脆伪造 SYN 消息中的 **Source IP**，使 B 反馈的 **SYN-ACK** 消息石沉大海，导致 B 被大量注定不能完成的半开连接占据，直到资源耗尽，停止响应正常的连接请求。

## <span style="font-size: inherit;color: inherit;line-height: inherit;">3 UDP Flooding</span>

**UDP** 洪泛也是一种拒绝服务攻击，将大量的用户数据报协议（**UDP**）数据包发送到目标服务器，目的是压倒该设备的处理和响应能力。防火墙保护目标服务器也可能因 **UDP** 泛滥而耗尽，从而导致对合法流量的拒绝服务。
> UDP Flood 攻击如何工作？

**UDP Flood** 主要通过利用服务器响应发送到其中一个端口的 **UDP** 数据包所采取的步骤。在正常情况下，当服务器在特定端口接收到 **UDP** 数据包时，会经过两个步骤：

*   服务器首先检查是否正在运行正在侦听指定端口的请求的程序。

*   如果没有程序在该端口接收数据包，则服务器使用 **ICMP**（ping）数据包进行响应，以通知发送方目的地不可达。

举个例子。假设今天要联系酒店的小蓝，酒店客服接到电话后先查看房间的列表来确保小蓝在客房内，随后转接给小蓝。

首先，接待员接收到呼叫者要求连接到特定房间的电话。接待员然后需要查看所有房间的清单，以确保客人在房间中可用，并愿意接听电话。碰巧的是，此时如果突然间所有的电话线同时亮起来，那么他们就会很快变得不堪重负了。

当服务器接收到每个新的 **UDP** 数据包时，它将通过步骤来处理请求，并利用该过程中的服务器资源。发送 **UDP** 报文时，每个报文将包含源设备的 **IP** 地址。在这种类型的 **DDoS** 攻击期间，攻击者通常不会使用自己的真实 **IP** 地址，而是会欺骗 **UDP** 数据包的源 **IP** 地址，从而阻止攻击者的真实位置被暴露并潜在地饱和来自目标的响应数据包服务器。

由于目标服务器利用资源检查并响应每个接收到的 **UDP** 数据包的结果，当接收到大量 **UDP** 数据包时，目标的资源可能会迅速耗尽，导致对正常流量的拒绝服务。
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwyIosXYguAxw5ibDk0icbFqRfJpVPvjMEZ9GTNcTqicTVtEcEicUPS5SKPg/640?wx_fmt=png)</figure>> 如何缓解&nbsp;**UDP&nbsp;**洪水攻击？

大多数操作系统部分限制了 **ICMP** 报文的响应速率，以中断需要 ICMP 响应的 **DDoS** 攻击。这种缓解的一个缺点是在攻击过程中，合法的数据包也可能被过滤。如果 **UDP Flood** 的容量足够高以使目标服务器的防火墙的状态表饱和，则在服务器级别发生的任何缓解都将不足以应对目标设备上游的瓶颈。

## <span style="font-size: inherit;color: inherit;line-height: inherit;">4 TCP 重置攻击</span>

在 **TCP** 重置攻击中，攻击者通过向通信的一方或双方发送伪造的消息，告诉它们立即断开连接，从而使通信双方连接中断。正常情况下，如果客户端发现到达的报文段对于相关连接而言是不正确的，**TCP** 就会发送一个重置报文段，从而导致 **TCP** 连接的快速拆卸。

**TCP** 重置攻击利用这一机制，通过向通信方发送伪造的重置报文段，欺骗通信双方提前关闭 TCP 连接。如果伪造的重置报文段完全逼真，接收者就会认为它有效，并关闭 **TCP** 连接，防止连接被用来进一步交换信息。服务端可以创建一个新的 **TCP** 连接来恢复通信，但仍然可能会被攻击者重置连接。万幸的是，攻击者需要一定的时间来组装和发送伪造的报文，所以一般情况下这种攻击只对长连接有杀伤力，对于短连接而言，你还没攻击呢，人家已经完成了信息交换。

从某种意义上来说，伪造 **TCP** 报文段是很容易的，因为 **TCP/IP** 都没有任何内置的方法来验证服务端的身份。有些特殊的 IP 扩展协议（例如 `IPSec`）确实可以验证身份，但并没有被广泛使用。客户端只能接收报文段，并在可能的情况下使用更高级别的协议（如 `TLS`）来验证服务端的身份。但这个方法对 **TCP** 重置包并不适用，因为 **TCP** 重置包是 **TCP** 协议本身的一部分，无法使用更高级别的协议进行验证。

## <span style="font-size: inherit;color: inherit;line-height: inherit;">5. 模拟攻击</span>
> 以下实验是在 `OSX` 系统中完成的，其他系统请自行测试。

现在来总结一下伪造一个 **TCP** 重置报文要做哪些事情：

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">嗅探通信双方的交换信息。</span>

*   截获一个 `ACK` 标志位置为&nbsp;1 的报文段，并读取其 `ACK` 号。

*   伪造一个 TCP 重置报文段（`RST` 标志位置为 1），其序列号等于上面截获的报文的 `ACK` 号。这只是理想情况下的方案，假设信息交换的速度不是很快。大多数情况下为了增加成功率，可以连续发送序列号不同的重置报文。

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">将伪造的重置报文发送给通信的一方或双方，使其中断连接。</span>

为了实验简单，我们可以使用本地计算机通过 `localhost` 与自己通信，然后对自己进行 TCP 重置攻击。需要以下几个步骤：

*   在两个终端之间建立一个 TCP 连接。

*   编写一个能嗅探通信双方数据的攻击程序。

*   修改攻击程序，伪造并发送重置报文。

下面正式开始实验。
> 建立 TCP 连接

可以使用 netcat 工具来建立 TCP 连接，这个工具很多操作系统都预装了。打开第一个终端窗口，运行以下命令：
<precode language="" precodenum="0"></precode>

这个命令会启动一个 TCP 服务，监听端口为 `8000`。接着再打开第二个终端窗口，运行以下命令：
<precode language="" precodenum="1"></precode>

该命令会尝试与上面的服务建立连接，在其中一个窗口输入一些字符，就会通过 TCP 连接发送给另一个窗口并打印出来。
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_gif/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwofraoxJ9CpicTG5yBHVN3IcvW1TuP5Mte5yr8Ng3msVaBNnic1e9YkJA/640?wx_fmt=gif "img")<figcaption style="line-height: inherit;margin-top: 10px;text-align: center;color: rgb(153, 153, 153);font-size: 0.7em;">
</figcaption></figure>> 嗅探流量

编写一个攻击程序，使用 Python 网络库 `scapy` 来读取两个终端窗口之间交换的数据，并将其打印到终端上。代码的核心是调用 `scapy` 的嗅探方法：
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIw9bofnrQ1sSSV1kBDy0Fxibofx9cMdGvhmMaWptdGuSj0zibQREjrvFxw/640?wx_fmt=png)</figure>

这段代码告诉 `scapy` 在 `lo0` 网络接口上嗅探数据包，并记录所有 TCP 连接的详细信息。

*   **iface** : 告诉 scapy 在 `lo0`（localhost）网络接口上进行监听。

*   **lfilter** : 这是个过滤器，告诉 scapy 忽略所有不属于指定的 TCP 连接（通信双方皆为 `localhost`，且端口号为 `8000`）的数据包。

*   **prn** : scapy 通过这个函数来操作所有符合 `lfilter` 规则的数据包。上面的例子只是将数据包打印到终端，下文将会修改函数来伪造重置报文。

*   **count** : scapy 函数返回之前需要嗅探的数据包数量。> 发送伪造的重置报文

下面开始修改程序，发送伪造的 TCP 重置报文来进行 TCP 重置攻击。根据上面的解读，只需要修改 prn 函数就行了，让其检查数据包，提取必要参数，并利用这些参数来伪造 TCP 重置报文并发送。

例如，假设该程序截获了一个从（`src_ip`, `src_port`）发往 （`dst_ip`, `dst_port`）的报文段，该报文段的 ACK 标志位已置为 1，ACK 号为 `100,000`。攻击程序接下来要做的是：

*   由于伪造的数据包是对截获的数据包的响应，所以伪造数据包的源 `IP/Port` 应该是截获数据包的目的 `IP/Port`，反之亦然。

*   将伪造数据包的 `RST` 标志位置为 1，以表示这是一个重置报文。

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">将伪造数据包的序列号设置为截获数据包的 ACK 号，因为这是发送方期望收到的下一个序列号。</span>

*   调用 `scapy` 的 `send` 方法，将伪造的数据包发送给截获数据包的发送方。

对于我的程序而言，只需将这一行取消注释，并注释这一行的上面一行，就可以全面攻击了。按照步骤 1 的方法设置 TCP 连接，打开第三个窗口运行攻击程序，然后在 TCP 连接的其中一个终端输入一些字符串，你会发现 TCP 连接被中断了！
> 进一步实验

1.  可以继续使用攻击程序进行实验，将伪造数据包的序列号加减 1 看看会发生什么，是不是确实需要和截获数据包的 `ACK` 号完全相同。

2.  打开 `Wireshark`，监听 lo0 网络接口，并使用过滤器 `ip.src == 127.0.0.1 &amp;amp;&amp;amp; ip.dst == 127.0.0.1 &amp;amp;&amp;amp; tcp.port == 8000` 来过滤无关数据。你可以看到 TCP 连接的所有细节。

3.  <span style="font-size: inherit;color: inherit;line-height: inherit;">在连接上更快速地发送数据流，使攻击更难执行。</span>

## <span style="font-size: inherit;color: inherit;line-height: inherit;">6 中间人攻击</span>

猪八戒要向小蓝表白，于是写了一封信给小蓝，结果第三者小黑拦截到了这封信，把这封信进行了篡改，于是乎在他们之间进行搞破坏行动。这个马文才就是中间人，实施的就是中间人攻击。好我们继续聊聊什么是中间人攻击。
> 什么是中间人

中间人攻击英文名叫 Man-in-the-MiddleAttack，简称「MITM攻击」。指攻击者与通讯的两端分别创建独立的联系，并交换其所收到的数据，使通讯的两端认为他们正在通过一个私密的连接与对方直接对话，但事实上整个会话都被攻击者完全控制。我们画一张图：
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwiaZADBplJPnIicicsEHmbdx9TQe3HT7LTxW4FibfN7aWiaHUr5bv1IHAx9Q/640?wx_fmt=png "中间人")<figcaption style="line-height: inherit;margin-top: 10px;text-align: center;color: rgb(153, 153, 153);font-size: 0.7em;">中间人</figcaption></figure>

从这张图可以看到，中间人其实就是攻击者。通过这种原理，有很多实现的用途，比如说，你在手机上浏览不健康网站的时候，手机就会提示你，此网站可能含有病毒，是否继续访问还是做其他的操作等等。
> 中间人攻击的原理

举个例子，我和公司签了一份劳动合同，双方各执一份合同。不晓得哪个可能改了合同内容，不知道真假了，怎么搞？只好找专业的机构来鉴定，自然就要花钱。

在安全领域有句话：**我们没有办法杜绝网络犯罪，只好想办法提高网络犯罪的成本**。既然没法杜绝这种情况，那我们就想办法提高作案的成本，今天我们就简单了解下基本的网络安全知识，也是面试中的高频面试题了。

为了避免双方说活不算数的情况，双方引入第三家机构，将合同原文给可信任的第三方机构，只要这个机构不监守自盗，合同就相对安全。
> 如果第三方机构内部不严格或容易出现纰漏

虽然我们将合同原文给第三方机构了，为了防止内部人员的更改，需要采取什么措施呢？

一种可行的办法是引入摘要算法，即合同和摘要一起。为了简单地理解摘要。大家可以想象这个摘要为一个函数，这个函数对原文进行了加密，会产生一个唯一的散列值，一旦原文发生一点点变化，那么这个散列值将会变化。
> 有哪些常用的摘要算法呢？

目前比较常用的加密算法有消息摘要算法和安全散列算法(**SHA**)。**MD5** 是将任意长度的文章转化为一个 128 位的散列值，可是在 2004 年，**MD5** 被证实了容易发生碰撞，即两篇原文产生相同的摘要。这样的话相当于直接给黑客一个后门，轻松伪造摘要。

所以在大部分的情况下都会选择 SHA 算法。
> 出现内鬼了怎么办？

看似很安全的场面了，理论上来说杜绝了篡改合同的做法。主要某个员工同时具有修改合同和摘要的权利，那搞事儿就是时间的问题了，毕竟没哪个系统可以完全地杜绝员工接触敏感信息，除非敏感信息都不存在。所以能不能考虑将合同和摘要分开存储呢？
> 那如何确保员工不会修改合同呢？

这确实蛮难的，不过办法总比困难多。我们将合同放在双方手中，摘要放在第三方机构，篡改难度进一步加大。
> 那么员工万一和某个用户串通好了呢？

看来放在第三方的机构还是不好使，同样存在不小风险。所以还需要寻找新的方案，这就出现了数字签名和证书。
> 数字证书和签名

同样的，举个例子。Sum 和 Mike 两个人签合同。Sum 首先用 **SHA** 算法计算合同的摘要，然后用自己私钥将摘要加密，得到数字签名。Sum 将合同原文、签名，以及公钥三者都交给 Mike。
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIw37aPMmCib42lddMz5nwnpCiadEFZOkukX9smhJANMLc4UFPHfbu5xOSw/640?wx_fmt=png)</figure>

如果 Sum 想要证明合同是 Mike 的，那么就要使用 Mike 的公钥，将这个签名解密得到摘要 x，然后 Mike 计算原文的 sha 摘要 Y，随后对比 x 和 y，如果两者相等，就认为数据没有被篡改。

在这样的过程中，Mike 是不能更改 Sum 的合同，因为要修改合同不仅仅要修改原文还要修改摘要，修改摘要需要提供 Mike 的私钥，私钥即 Sum 独有的密码，公钥即 Sum 公布给他人使用的密码。

总之，公钥加密的数据只能私钥可以解密。私钥加密的数据只有公钥可以解密，这就是非对称加密。
> 对称与非对称加密

隐私保护？不是吓唬大家，信息是透明的兄die，不过尽量去维护个人的隐私吧，今天学习对称加密和非对称加密。

大家先读读这个字"钥"，是读"yao"，我以前也是，其实读"yue"。
> 对称加密

对称加密，顾名思义，加密方与解密方使用同一钥匙(秘钥)。具体一些就是，发送方通过使用相应的加密算法和秘钥，对将要发送的信息进行加密；对于接收方而言，使用解密算法和相同的秘钥解锁信息，从而有能力阅读信息。
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwgmbibusKuJ7XyqoHPhbniaz2G38fn15Y8sXdkfPhr0npLMb4Feibt51LA/640?wx_fmt=png)</figure>> 常见的对称加密算法

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">DES</span>> DES 使用的密钥表面上是 64 位的，然而只有其中的 56 位被实际用于算法，其余 8 位可以被用于奇偶校验，并在算法中被丢弃。因此，**DES** 的有效密钥长度为 56 位，通常称 **DES** 的密钥长度为 56 位。假设秘钥为 56 位，采用暴力破Jie的方式，其秘钥个数为 2 的 56 次方，那么每纳秒执行一次解密所需要的时间差不多1年的样子。当然，没人这么干。**DES** 现在已经不是一种安全的加密方法，主要因为它使用的 56 位密钥过短。<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_jpg/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwGGXlCdAg38r5aibpsv3cCNqGHiava5PQf0nWZkVPFTyctWicbfIOJqrlg/640?wx_fmt=jpeg)</figure>

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">IDEA</span>> 国际数据加密算法(International Data Encryption Algorithm)。秘钥长度 128 位，优点没有专利的限制。

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">AES</span>> 当 DES 被破解以后，没过多久推出了 **AES** 算法，提供了三种长度供选择，128 位、192 位和 256，为了保证性能不受太大的影响，选择 128 即可。

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">SM1 和 SM4</span>> 之前几种都是国外的，我们国内自行研究了国密 **SM1 **和 **SM4**。其中 S 都属于国家标准，算法公开。优点就是国家的大力支持和认可。

总结下：
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwSKJUqrAIKX3GZyvDR9CbeIJKSRrqLBczRAZwfZugAVWzs6ZE9bwMuw/640?wx_fmt=png)</figure>> 非对称算法

在对称加密中，发送方与接收方使用相同的秘钥。那么在非对称加密中则是发送方与接收方使用的不同的秘钥。其主要解决的问题是防止在秘钥协商的过程中发生泄漏。比如在对称加密中，小蓝将需要发送的消息加密，然后告诉你密码是 123balala，ok，对于其他人而言，很容易就能劫持到密码是 123balala。那么在非对称的情况下，小蓝告诉所有人密码是 123balala，对于中间人而言，拿到也没用，因为没有私钥。所以，非对称密钥其实主要解决了密钥分发的难题。如下图：
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwqrXFic9Gggt8s2ibebQljzB1oXKR2VPfZ73Jrk6wtPnPbPlvmYc8b3GA/640?wx_fmt=png "非对称算法")<figcaption style="line-height: inherit;margin-top: 10px;text-align: center;color: rgb(153, 153, 153);font-size: 0.7em;">非对称算法</figcaption></figure>> 其实我们经常都在使用非对称加密，比如使用多台服务器搭建大数据平台 hadoop，为了方便多台机器设置免密登录，是不是就会涉及到秘钥分发。再比如搭建 docker 集群也会使用相关非对称加密算法。<section style="margin-bottom: 15px;">**常见的非对称加密**</section>

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">RSA（RSA 加密算法，RSA Algorithm）</span>> 优势是性能比较快，如果想要较高的加密难度，需要很长的秘钥。

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">ECC</span>> 基于椭圆曲线提出。是目前加密强度最高的非对称加密算法。

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">SM2</span>> 同样基于椭圆曲线问题设计。最大优势就是国家认可和大力支持。

三种对比：
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwhdEO0kXeZwDnJhK2jltZw8J3kVeJcslpdfqf0g7deSBvvAwuObpx7g/640?wx_fmt=png)</figure>> 散列算法

这个大家应该更加熟悉了，比如我们平常使用的 MD5 校验，在很多时候，我并不是拿来进行加密，而是用来获得唯一性 ID。在做系统的过程中，存储用户的各种密码信息，通常都会通过散列算法，最终存储其散列值。
> 常见的散列

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">MD5</span>> MD5 可以用来生成一个 128 位的消息摘要，它是目前应用比较普遍的散列算法。虽然，因为算法的缺陷，它的唯一性已经被破解了，但是大部分场景下，这并不会构成安全问题。但是，如果不是长度受限（32 个字符），我还是不推荐你继续使用 **MD5** 的。

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">SHA</span>> 安全散列算法。**SHA **分为 **SHA1** 和 **SH2** 两个版本。该算法的思想是接收一段明文，然后以一种不可逆的方式将它转换成一段（通常更小）密文，也可以简单地理解为取一串输入码（称为预映射或信息），并把它们转化为长度较短、位数固定的输出序列即散列值（也称为信息摘要或信息认证代码）的过程。

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">SM3</span>> 国密算法&nbsp;**SM3**。加密强度和 SHA-256 差不多。主要是受到国家的支持。

总结：
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwl4HLPPrRXALx8EREuoMy7xjJiauy5y2DRdI8VV20ffiboIU7nHKCZGQQ/640?wx_fmt=png)</figure>

至此，总结下，大部分情况下使用对称加密，具有比较不错的安全性。如果需要分布式进行秘钥分发，考虑非对称。如果不需要可逆计算则散列算法。
> 问题还有，此时如果 Sum 否认给过 Mike 的公钥和合同，不久 gg 了。

所以需要 Sum 说过的话做过的事儿有足够的信誉，这就引入了第三方机构和证书机制。

证书之所以会有信用，是因为证书的签发方拥有信用。所以如果 Sum 想让 Mike 承认自己的公钥，Sum 不会直接将公钥给 Mike ，而是由第三方机构提供含有公钥的证书。如果 Mike 也信任这个机构，法律都认可，那 ok，信任关系成立。
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwmvNGeFcfzeGAlLMyN6cqBCXpRYGrZibFEWFv6ibqYbSIZgIgmuhU08Zg/640?wx_fmt=png)</figure>

如上图所示，Sum 将自己的申请提交给机构，产生证书的原文。机构用自己的私钥签名 Sum 的申请原文（先根据原文内容计算摘要，再用私钥加密），得到带有签名信息的证书。Mike 拿到带签名信息的证书，通过第三方机构的公钥进行解密，获得 Sum 证书的摘要、证书的原文。有了 Sum 证书的摘要和原文，Mike 就可以进行验签。验签通过，Mike 就可以确认 Sum 的证书的确是第三方机构签发的。

用上面这样一个机制，合同的双方都无法否认合同。这个解决方案的核心在于需要第三方信用服务机构提供信用背书。这里产生了一个最基础的信任链，如果第三方机构的信任崩溃，比如被黑客攻破，那整条信任链条也就断裂了。

为了让这个信任条更加稳固，就需要环环相扣，打造更长的信任链，避免单点信任风险。
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIwl9XhNVOOLQhKzkG8hMQklGjqOFlC7P87vmbnzEmtpRUgCWcPJaBiaEw/640?wx_fmt=png)</figure>

上图中，由信誉最好的根证书机构提供根证书，然后根证书机构去签发二级机构的证书；二级机构去签发三级机构的证书；最后由三级机构去签发 Sum 证书。

如果要验证 Sum 证书的合法性，就需要用三级机构证书中的公钥去解密 Sum 证书的数字签名。

如果要验证三级机构证书的合法性，就需要用二级机构的证书去解密三级机构证书的数字签名。

如果要验证二级结构证书的合法性，就需要用根证书去解密。

以上，就构成了一个相对长一些的信任链。如果其中一方想要作弊是非常困难的，除非链条中的所有机构同时联合起来，进行欺诈。
> 中间人攻击如何避免?

既然知道了中间人攻击的原理也知道了他的危险，现在我们看看如何避免。相信我们都遇到过下面这种状况：
<figure style="font-size: inherit;color: inherit;line-height: inherit;">![图片](https://mmbiz.qpic.cn/mmbiz_png/WUrZckMPh54ibk9Dxib1ZNwvvdnEWbHsIw39VibH175nzicsjnImlVDttGjoUfXybibibvrs7JTTSp7ckdtwq8d9DwQg/640?wx_fmt=png)</figure>

出现这个界面的很多情况下，都是遇到了中间人攻击的现象，需要对安全证书进行及时地监测。而且大名鼎鼎的 github 网站，也曾遭遇过中间人攻击：

想要避免中间人攻击的方法目前主要有两个：

*   客户端不要轻易相信证书：因为这些证书极有可能是中间人。

*   App 可以提前预埋证书在本地：意思是我们本地提前有一些证书，这样其他证书就不能再起作用了。

## <span style="font-size: inherit;color: inherit;line-height: inherit;">7 DDOS</span>

通过上面的描述，好多种攻击都是 **DDOS** 攻击，所以简单总结下这个攻击相关内容。

其实，像全球互联网各大公司，均遭受过大量的 **DDoS&nbsp;**攻击。

2018 年，GitHub 在一瞬间遭到高达 1.35Tbps 的带宽攻击。这次 DDoS 攻击几乎可以堪称是互联网有史以来规模最大、威力最大的 DDoS 攻击了。在 GitHub 遭到攻击后，仅仅一周后，DDoS 攻击又开始对 Google、亚马逊甚至 Pornhub 等网站进行了 DDoS 攻击。后续的 DDoS 攻击带宽最高也达到了 1Tbps。
> 那 DDoS 攻击究竟是什么？

DDos 全名 Distributed Denial of Service，翻译成中文就是**分布式拒绝服务**。指的是处于不同位置的多个攻击者同时向一个或数个目标发动攻击，是一种分布的、协同的大规模攻击方式。单一的 DoS 攻击一般是采用一对一方式的，它利用网络协议和操作系统的一些缺陷，采用**欺骗和伪装**的策略来进行网络攻击，使网站服务器充斥大量要求回复的信息，消耗网络带宽或系统资源，导致网络或系统不胜负荷以至于瘫痪而停止提供正常的网络服务。
> 举个例子

我开了一家有五十个座位的重庆火锅店，由于用料上等，童叟无欺。平时门庭若市，生意特别红火，而对面二狗家的火锅店却无人问津。二狗为了对付我，想了一个办法，叫了五十个人来我的火锅店坐着却不点菜，让别的客人无法吃饭。

上面这个例子讲的就是典型的 DDoS 攻击，一般来说是指攻击者利用“肉鸡”对目标网站在较短的时间内发起大量请求，大规模消耗目标网站的主机资源，让它无法正常服务。在线游戏、互联网金融等领域是 DDoS 攻击的高发行业。

攻击方式很多，比如 **ICMP Flood**、**UDP Flood**、**NTP Flood**、**SYN Flood**、**CC 攻击**、**DNS Query Flood&nbsp;**等等。
> SYN Flood 进行 DDoS 攻击的实现原理**

**SYN Flood** 是一种利用 **TCP** 协议缺陷，发送大量伪造的 **TCP** 连接请求，从而使得被攻击方资源耗尽（CPU 满负荷或内存不足）的攻击方式。

一次正常的建立 **TCP** 连接，需要三次握手：客户端发送 **SYN** 报文，服务端收到请求并返回报文表示接受，客户端也返回确认，完成连接。

**SYN Flood** 就是用户向服务器发送报文后突然死机或掉线，那么服务器在发出应答报文后就无法收到客户端的确认报文（第三次握手无法完成），这时服务器端一般会重试并等待一段时间后再丢弃这个未完成的连接。

一个用户出现异常导致服务器的一个线程等待一会儿并不是大问题，但恶意攻击者大量模拟这种情况，服务器端为了维护数以万计的半连接而消耗非常多的资源，结果往往是无暇理睬客户的正常请求，甚至崩溃。从正常客户的角度看来，网站失去了响应，无法访问。
> 如何应对 DDoS 攻击？

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">高防服务器</span>

还是拿开的重庆火锅店举例，高防服务器就是我给重庆火锅店增加了两名保安，这两名保安可以保护店铺不受流氓骚扰，并且还会定期在店铺周围巡逻防止流氓骚扰。

高防服务器主要是指能独立硬防御 50Gbps 以上的服务器，能够帮助网站拒绝服务攻击，定期扫描网络主节点等，这东西是不错，就是贵~

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">黑名单</span>

面对火锅店里面的流氓，我一怒之下将他们拍照入档，并禁止他们踏入店铺，但是有的时候遇到长得像的人也会禁止他进入店铺。这个就是设置黑名单，此方法秉承的就是“错杀一千，也不放一百”的原则，会封锁正常流量，影响到正常业务。

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">DDoS 清洗</span>

**DDos** 清洗，就是我发现客人进店几分钟以后，但是一直不点餐，我就把他踢出店里。

**DDoS** 清洗会对用户请求数据进行实时监控，及时发现 **DOS **攻击等异常流量，在不影响正常业务开展的情况下清洗掉这些异常流量。

*   <span style="font-size: inherit;color: inherit;line-height: inherit;">CDN 加速</span>

CDN 加速，我们可以这么理解：为了减少流氓骚扰，我干脆将火锅店开到了线上，承接外卖服务，这样流氓找不到店在哪里，也耍不来流氓了。

在现实中，CDN 服务将网站访问流量分配到了各个节点中，这样一方面隐藏网站的真实 IP，另一方面即使遭遇 **DDoS** 攻击，也可以将流量分散到各个节点中，防止源站崩溃。

## <span style="font-size: inherit;color: inherit;line-height: inherit;">总结</span>

计算机网络涉及的知识点较多，文中也就算是提了一下，更深层次的理解还需要大家去看相应的书籍，感觉看了这一篇，当面试官问 DDOS 或者 TCP 涉及哪些攻击技术知识点的时候，能够回答出来就好了。
</section>

<span style="color: rgb(136, 136, 136);font-size: 14px;">&lt;END&gt;
</span>

<span style="color: rgb(136, 136, 136);font-size: 14px;">来源 |&nbsp;暖蓝笔记</span>

<span style="color: rgb(136, 136, 136);font-size: 14px;">作者 |&nbsp;蓝蓝</span>
</div>
