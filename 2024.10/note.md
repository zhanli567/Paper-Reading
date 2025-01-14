# 智能网联车网络安全研究综述

[原文PDF](./智能网联车网络安全研究综述_吴武飞.pdf)

    首先介绍了智能网联车的结构现状和特点，阐述了车载网络安全面临的设计约束和挑战。其次结合车载网络当前面临的功能安全和信息安全问题，介绍了今年来国内外最新研究进展。最后从车载网络结构特点出发，从标准建设、功能安全和信息安全3个方面，指出了一些重要的研究方向。

## 一、引言

    智能网联车电子系统逐步演变为集感知、计算、网络和控制为一体的信息物理融合系统，系统复杂化和对外通信接口的增加会使车载网络更易受到攻击。汽车安全问题包含功能安全和信息安全两方面。出于成本和性能的均衡考虑，当前车载网络存在带宽受限、强实时和确定性时延的要求和特点。

## 二、背景介绍

#### 2.1 智能网联车车载网络介绍

    智能网联车是一个异构分布式实时系统，车载电子控制单元ECU由异构网络（控制器局域网络CAN、本地互联网络LIN）连接，主要特征有：丰富的对外接口、大量实时数据、异构网络环境、信息安全保护机制缺乏。

![image-20241028093023357](https://s2.loli.net/2024/10/29/7nkUfhJbLscQ8aT.png)

![image-20241028093111692](https://s2.loli.net/2024/10/29/EDcGUQnjaysbJKh.png)

![image-20241028093126429](https://s2.loli.net/2024/10/29/qXEbyQC32R9pIBN.png)

#### 2.2 车载网络的分类

![image-20241028093148797](https://s2.loli.net/2024/10/29/OuLofliy8x7Ec4D.png)

    车载网络可分为时间触发TT和事件触发ET。

    TT是指以时间点为通信触发条件，一般通过定时和时间同步方式实现。

    ET是指通信触发条件，即某一事件发生。如汽车安全气囊系统检测到碰撞，通过触发传感器所在ECU发送数据帧引爆气囊。

当前车载网络中TT型网络主要有TTCAN、TTEthernet、TTP/C等。TT型车载网络具有带宽高、传输时延确定的特点，弥补了ET型在确定性时延的不足。

## 三、车载网络信息安全问题分析

#### 3.1 严峻的信息安全威胁

![image-20241028093223518](https://s2.loli.net/2024/10/29/q2vnz74kQNR5H1l.png)

    直接物理接入攻击主要通过非法接入CAN、车载诊断系统OBD诊断接口等方式。

    近距离无线攻击主要通过蓝牙和无线传感器信道非法接入的方式。

    远程无限攻击主要通过WIFI和移动数字蜂窝网络端口实现非法接入。

#### 3.2 缺乏信息安全保障的车载网络

    现有的车载网络协议如CAN和FlexRay等在设计之初缺乏安全机制设计，使得车载网络易受到嗅探、伪造、修改和重放等类型的攻击。其脆弱性体现在以下方面：

    脆弱的接入控制：物理层为双绞线或同轴电缆，接入简单、缺乏异常接入检测功能。

    无数据加密保障：内部消息传输只根据功能编码，缺乏加密保护。

    无消息认证机制：消息仅通过消息ID进行标定和作为接收过滤，易遭受拒绝服务DoS、重放、伪造等攻击。

#### 3.3 丰富的网络安全攻击入口

    1.来自传感层（物理层）的攻击。未来汽车配备激光雷达、毫米波雷达、摄像头和GPS等传感器，通过物理层攻击将成为新威胁。

    2.非法访问（数据链路层）。车载网络缺乏数据加密和消息验证，攻击者一旦访问网络设计即可实施攻击。数据链路层攻击模式有帧注入、帧伪造、帧嗅探、暂停和DoS攻击。

    3.来自接口（应用层）的攻击。攻击入口包括蓝牙、OBD\_II、WIFI等。此类攻击没有非法访问节点和明显数据帧异常难以被检测。针对此类攻击，当前研究集中于机器学习的入侵检测方法设计，存在计算资源消耗过大、缺乏测试数据集及模型评估等问题。

#### 3.4 功能安全保障下的信息安全问题

![image-20241028093352015](https://s2.loli.net/2024/10/29/2OFrNbuDCRWAjqY.png)

    总结得出四点功能安全保障下的车载网络信息安全设计面临的挑战和约束：

    1.计算、存储及通信带宽资源的约束。

    2.复杂异构的软硬件结构不仅给功能安全和信息安全增加了不确定因素，也给系统功能安全保障测试验证增加难度。

    3.成本和性能的均衡考虑，ECU的计算和存储资源有限，部署的高成本可能导致网络安全部署被给予低优先级，由于成本约束，传统信息的网络信息安全增强方案无法部署于汽车环境。

    4.车载网络对功能安全设计的约束表现为消息传输的实时性、端到端时延边界、系统任务可调度性等。针对可调度性分析的研究主要集中在探索通信时延的上界、网络消息可调度性分析、满足确定性时延分析等方面。

## 四、车载网络信息安全增强技术研究进展

#### 4.1 车载网络数据加密技术

    传统的消息加密与认证技术在车载网络环境下面临体系结构异构、带宽和计算资源受限等问题。为减少加密运算带来的额外时间开销，通常采用轻量化、硬件加速等方式，如利用可编程逻辑器件进行高级加密标准AES、椭圆曲线密码编码学ECC运算加速、通过即现场可编程门阵列PFGA实现裁剪版的哈希算法、将多个消息传输一个MAC等。

    针对计算资源紧张和i西澳西加密带来的时间开销问题，Wang等采用添加硬件模块方式解决加密算法时间问题，缺点增加了硬件部署的成本。

    应对多种车载ECU的漏洞和攻击模型，Siddiqui等提出基于硬件的安全可信框架，在车载CAN上实现基于轻量级物理不可克隆函数PUF的双向认证和非安全通信信道上的安全加密，缺点是导致网络协议异常复杂。

#### 4.2 车载网络消息认证技术

    近年来，车载CAN的多种轻量级消息认证协议被提出保护车辆免受伪装攻击。该协议最初由Herrewege等提出。Jo等提出MAuth-CAN可在不修改CAN硬件控制器的同时实现网络带宽消耗与防止伪装攻击之间的均衡。Kang提出在CAN中使用单向哈希链的轻量级源认证协议，具有攻击弹性树算法，可通过ＥＣＵ的固件更新实现部署。

    轻量级消息认证协议可解决CAN协议缺乏安全认证设计的问题，现存在问题在于如何在提高消息认证安全性的同时避免因通信带宽消耗而导致消息可调度引起的功能可靠和实时问题。

#### 4.3 车载网络异常入侵检测技术

    相较于消息加密、访问控制、协议认证等信息安全增强手段，入侵检测具有占用带宽资源小、便于现有车辆部署的特点，更适合资源和成本受限的车载网络。

![image-20241028093416216](https://s2.loli.net/2024/10/29/HXWQVtBi18qPjDT.png)

    基于特征观察的检测方法针对特定攻击模型能取得较高的检测精度，具有响应时间短、网络带宽开销小的特点。现有研究中存在以下问题：检测方法往往针对特定攻击模型；检测效果稳健性不强（有诸多前提条件，缺乏对汽车状态的感知）；缺乏对检测响应时间的评估及对功能安全保障的影响。

    现有基于信息理论的车载网络入侵检测方法研究往往忽略了汽车不同状态带来的车载网络信息熵抖动对检测结果的影响，其检测模型在有限汽车状态下具有较高的检测精度，但对不同汽车的稳健性有待提高。

    机器学习对于车载网络未知攻击模型的入侵检测具有较好的效果，但在车载网中，现有基于机器学习的入侵检测方法在如何降低计算复杂度和对车载网络通信带宽的消耗上是一个有待解决的问题，同时提高检测精度、降低误报率、缩短响应时间和提高稳健性也是改善的方向。

![image-20241028093438439](https://s2.loli.net/2024/10/29/uHPvE4tZdbwLhSA.png)

![image-20241028093444693](https://s2.loli.net/2024/10/29/hlyaBbAWLxnVY7j.png)

## 五、分析和总结

    结合智能网联车发展趋势及当前车载网络安全方面的最新研究进展，提出了一些开放性问题。

**5.1 如何提高入侵检测精度、降低响应时间**

**5.2 如何实现精准的网络安全测试评估**

**5.3 如何应对未知的智能网联车网络攻击**

**5.4 如何实现网络安全增强与资源消耗的均衡**

**5.5 如何制定及时有效的智能网联车信息安全标准**

## 六、结束语

    本文首先介绍了智能网联车中车载网络协议现状及分类情况，随后总结了当前车载网络安全问题对比分析了车载网络安全增强技术现状，最后对未来车载网络安全技术的发展和研究进行了总结和展望。

# 智能网联汽车的车载网络攻防技术研究进展

[原文PDF](./智能网联汽车的车载网络攻防技术研究进展_陈博言.pdf)

    智能网联车是一种由ECU组成的复杂分布式异构系统。攻击者可以从各个接口攻击智能网联车，故车载网络安全成为安全研究的焦点之一。在介绍网联汽车整体结构、ECU、CAN总线和车载诊断协议的基础上，首先介绍目前车载网络协议的逆向工程技术发展，然后从攻、防两个角度展开：一方面讲车载网络攻击向量和主要攻击技术，另一方面讲现有的防御技术，最后展望未来研究方向。

**关键词：**智能网联汽车；车载网络；逆向工程；入侵检测；协议安全增强

## 一、基础知识

#### 1.1 相关术语

![image-20241029115436975](https://s2.loli.net/2024/10/29/UCzcwNj6FdxA2MB.png)

#### 1.2 智能网联汽车整体结构

![image-20241029115531284](https://s2.loli.net/2024/10/29/el2NHLtKzMZDkbv.png)

#### 1.3 ECU和车载网络协议

**1.3.1 ECU**

![image-20241029115927005](https://s2.loli.net/2024/10/29/BSM4fZIw8DGHJTx.png)

**1.3.2 CAN协议**

![image-20241029115957505](https://s2.loli.net/2024/10/29/KlcN8BmYMZAwquT.png)

**1.3.3 车载诊断协议**

## 二、车载网络攻防研究方向

![image-20241029120323108](https://s2.loli.net/2024/10/29/aj2MLZuBW6FUxAd.png)

## 三、车载网络协议逆向

    汽车行业厂商出于各种原因，一般不公开其车载网络相关协议实现细节。无论是研究者还是攻击者，要想推测出消息的具体语义都绕不开车载网络协议的逆向。

#### 3.1 协议逆向过程

    CAN信号是车载网络协议逆向的基本单位，作为一个令牌(token)。令牌是车载网络协议逆向的基本单位，主要包括以下类型：(1)物理值：用于表示实时的车辆动态，如车速、转弯角等。(2)状态值：表示一组有限的状态，例如车门打开或关闭。(3)计数器：在特定范围内作为循环计数器的信号。(4)校验码：有效载荷还包括额外的校验码，通常作为有效载荷的最后一个信号。

    车载网络逆向的**输入**是原始的CAN数据流，获取CAN数据流最常用的方法是将CAN数据记录仪通过ODB-II接口连接到CAN总线上。车载网络逆向的**输出**是DBC格式的文件，DBC文件是一种CAN信号信息的可读文件，包含了CAN信号的位置、语义和格式以及取值范围等信息。车载网络协议逆向的**目的**是定位CAN信号在CAN数据帧中的位置，将CAN数据帧切分为CAN信号, 该过程称为**载荷令牌化**；然后再分析每一个CAN信号的语义和格式, 该过程称为**令牌解析**。

![image-20241029121436516](https://s2.loli.net/2024/10/29/ONoXfrPkw9YERuF.png)

#### 3.2 载荷令牌化

    载荷令牌化的目标是识别CAN帧的有效载荷中的每个CAN信号。相关方法可分为两类：

    (1)基于组合优化的载荷令牌化：基于组合优化的方法设置一个组合优化分数函数，在令牌组合候选集中选择使该分数函数最大的令牌切分组合。

    (2)基于比特翻转率的载荷令牌化：该方法思想是，不同CAN信号之间的比特翻转率很可能不同，一个CAN信号内的比特翻转率接近。

#### 3.3 令牌解析

    经过载荷令牌化过程，CAN信号在有效负载中的位置已知，但其语义含义和格式尚未被翻译。令牌解析阶段 将解析CAN信号的格式和语义，输出DBC文件。令牌解析相关工作可以分为如下3类：

    (1)基于PID注入的令牌解析：通过向OBD-II接口注入参数标识(PID)，并观察CAN数据流的变化，分析CAN 信号的语义。这是很多令牌解析的基础方法，一些其他类别的工作也需要结合基于PID注入的令牌解析方法。

    (2)基于语义分类的令牌解析：该方法利用语义相似的CAN信号组的内在属性，以及这些组之间语义的联系解析CAN信号。

    (3)基于配套应用的令牌解析：智能网联汽车的配套应用是运行在移动端和桌面端的应用程序，可以与车载网络进行交互。

#### 3.4 小结

![image-20241029122439714](https://s2.loli.net/2024/10/29/qGWK5T4MsDVgwaZ.png)

![image-20241029122455932](https://s2.loli.net/2024/10/29/auR2GckDtzKL5pV.png)

## 四、车载网络攻击技术

#### 4.1 概述

![image-20241029122914369](https://s2.loli.net/2024/10/29/eM7TAXIhG14sfzd.png)

![image-20241029122922907](https://s2.loli.net/2024/10/29/9q5mbRZOul6VUcr.png)

    部分攻击者入侵CAN总线后，可能执行以下恶意功能：(1)数据窃取，窃取驾驶者相关信息。(2)控制车辆，发送恶意CAN数据包破坏车辆驾驶行为。(3)数据欺骗，向驾驶员或自动驾驶系统反馈错误信息，导致错误的驾驶决策。

#### 4.2 攻击入口

**4.2.1 物理访问攻击**

    OBD-II接口是一种汽车故障检测和诊断接口，通过该接口可以获取车辆实时和历史数据，但其设计之初未考虑安全问题，攻击者可以利用该漏洞进行攻击。车载娱乐系统配备的USB接口一旦被攻击者获得了访问权限，也可以执行攻击。

**4.2.2 无线访问攻击**

    无线访问攻击可分为通过传感器的攻击、通过近程通信的攻击和通过远程通信的攻击。

**通过传感器的攻击：**

    智能网联车需要不同功能的传感器实时获取周围环境信息，这些传感器的测量结果作为自动驾驶系统的输入，对行驶安全至关重要。传感器攻击发生在自动驾驶的信息收集阶段。

    (1)摄像头欺骗攻击：摄像头是自动驾驶系统进行环境感知、即时定位与地图构建(SLAM) 的最重要传感器

    (2)雷达传感器欺骗攻击：激光雷达通过发射激光并捕获反射来计算与障碍物的距离，是智能网联汽车重要的传感器之一。激光雷达可获取周围环境的三维点云数据，并用于感知和识别障碍物、道路标志等关键任务。

**通过近程通信的攻击**

    智能网联汽车需要结合蓝牙、RFID等近程通信技术完成相应的功能，例如无钥匙进入等功能，这些近程通信接口也为攻击者带来了新的攻击面。

    (1)车载蓝牙攻击：一些研究者已经充分论证了蓝牙的安全威胁，然而针对车载蓝牙攻击的研究相对较少

    (2)无钥匙进入系统攻击：无钥匙进入系统通过无线射频技术(RFID)或蓝牙技术实现车辆的解锁和上锁功能，使车主无须金属钥匙即可打开汽车。针对传统汽车的无钥匙进入系统，已经有攻击者通过无线中继攻击恶意解锁并盗窃车辆的例子。随着车辆智能化程度不断提高，其暴露的攻击面不断增加。

**通过远程通信的攻击**

    智能网联车需要通过蜂窝网络等远程通信技术完成相应功能，这就给了远程攻击者提供了较大的攻击面。

    (1)WiFi攻击：WiFi是智能车进行OTA升级的重要入口，也往往被攻击者利用

    (2)蜂窝网络攻击：车主可通过手机远程操控智能车，若车主手机被黑客操控，黑客可控制车空App连接并访问汽车。

#### 4.3 攻击目标

    攻击者通过物理访问或无线访问方式入侵车载网络后，其最终目标是攻击车载网络及其组成部分如ECU。按攻击目标分类，最终目标可能是ECU或者CAN总线。

**4.3.1 针对ECU的攻击**

    (1)ECU伪装攻击：CAN总线具有广播的特性且CAN消息中不包含收发者的相关信息，如果攻击者可以访问CAN总线，则其可以获取总线上所有消息，在学习ECU的行为方式(如CANID，传输速率，CAN消息有效载荷的范围等)后，攻击者可以构造相同的信息冒充ECU发送消息。

    (2)ECU重刷攻击：重刷攻击指攻击者试图在智能车中修改ECU的软件或固件，可以通过物理接入ECU或者通过网络连接实现。

**4.3.2 针对CAN总线的攻击**

    (1)CAN重放攻击：目标是捕获CAN总线上的有效信息，不修改或者添加恶意payload后再重新发送该消息，造成CAN消息的延迟或不可用从而影响整个CAN总线。

    (2)CAN总线关闭攻击：是一种针对CAN总线的拒绝服务(DoS)攻击，目的是使CAN总线进入总线关闭状态，进而让通信受阻。攻击主要方式是向CAN总线发送大量的错误消息，使CAN控制器错误地认为总线上发生了严重的通信错误，触发总线关闭机制，导致整个CAN总线通信中断。

    (3)CAN消息篡改攻击：攻击者通过物理方式或者远程访问的方式对CAN总线上传输的数据进行篡改，发送篡改后的数据包来干扰车辆运行，执行恶意功能。

    (4)CAN消息注入攻击：攻击者使用其控制的恶意ECU模拟其他合法设备发送伪造的CAN消息，导致其他设备产生错误的行为。

#### 4.4小结

![image-20241029141921177](https://s2.loli.net/2024/10/29/67UXv4LzQc9neRl.png)

## 五、车载网络防御技术

#### 5.1 目标和挑战

    目标是抵御不同能力攻击者从各个层次发起的不同种类的车载网络攻击。攻击产生的主要原因是车载网络普通缺乏信息加密和认证机制。

![image-20241029142147688](https://s2.loli.net/2024/10/29/FPzUyt2DhiuOSC7.png)

    挑战主要有以下4点：(1)与现有协议的兼容性。(2)实时性约束。(3)ECU算力约束。(4)ECU源代码约束。

#### 5.2 车载网络入侵检测技术

**5.2.1 基于特征工程的入侵检测**

    (1)基于信号特征的入侵检测工作：ECU具备一些固定的信号特征如电压特征，恶意ECU无法改变电压这一硬件特征。此外，车载网络攻击还具有一些独特的信号特征，如时钟特征、信号长度等。

    (2)基于CAN消息的入侵检测：此类工作主要实现在消息层，其中一种方法是基于网络参数模型的车载网络入侵检测，通过检测CAN消息中的参数变化来检测潜在的入侵。该方法对计算资源要求较低，但对于消息注入攻击效果较差，因消息注入攻击可以是正常消息，其网络参数不会有任何变化，同时对非周期性的操作检测率很低。另一种方法是基于消息语义的入侵检测，其根据消息的语义和车辆状态、外部环境等信息判断消息是否为恶意。

    (3)基于信息熵的入侵检测：通过对网络流量的熵值进行分析来判断是否存在入侵行为。任何不正常的行为都可能导致网络熵值的显著变化。

**5.2.2 基于机器学习的入侵检测**

    (1)基于传统机器学习的入侵检测：传统的机器学习方法，包括支持向量机、决策树、随机森林和多层感知机，被广泛运用于车载网络入侵检测。缺点是计算复杂度较高，还需要大量的数据集来训练模型，而且有价值的数据集很少，尤其是有攻击或异常流量的数据集。

    (2)基于深度学习的入侵检测：与前者相比，避免了复杂的特征提取步骤。

#### 5.3 车载网络协议安全增强技术

**5.3.1 基于轻量级密码学的通信机密性增强**

    车载网络普遍缺乏机密性设计，CAN总线广播的特性且缺乏加密机制，导致了CAN总线容易遭受ECU伪装攻击、消息篡改攻击等。ECU的算力较低，且CAN实时性要求较高，因此无法使用传统开销较大的密码学算法。

**5.3.2 基于高效HMAC的身份鉴别和消息完整性增强**

    基于哈希的消息认证码是消息认证的重要方法之一，哈希函数是一类单向函数，具有不可逆性。在CAN标准中，没有消息认证机制，但每个消息发送方都包含一个唯一标识CANID，可根据CANID产生一个消息摘要，接收消息的ECU再根据该消息摘要进行校验，从而鉴别消息发送者的身份。

#### 5.4 小结

![image-20241029144256088](https://s2.loli.net/2024/10/29/Fd1zENrJGT59gWp.png)

![image-20241029144305251](https://s2.loli.net/2024/10/29/DUvsOLrbYHqFaRK.png)

    入侵检测研究还存在一些局限性，包括：

    (1)现有大多数入侵检测系统仅使用一种类型的车辆数据(如传感器、CAN帧或OBD-II消息)来检测异常，没有充分运用各类信息。

    (2)现有工作大多基于单一的技术或算法，没有很好地规避单一方法的缺点，多个方法混合使用，扬长避短，可能会达到更好的效果。

    (3)现有工作中大多数没有充分利用汽车的场景信息，汽车是一个与驾驶者和环境不断交互的系统，充分利用这些不断变化的场景信息对车载网络的入侵检测工作十分重要。

    (4)受限于时间和成本, 大多数现有工作的实验平台受限，测试不够充分。

![image-20241029144826228](https://s2.loli.net/2024/10/29/w6qxl7RFQ9TtKzv.png)

    车载网络协议安全增强技术还存在一些局限如：

    (1) 一些方案与现有CAN协议不兼容。车载网络协议安全增强方案不兼容导致厂商需要重新设计ECU的固件，对于供应商来说，推出新固件的成本是很高的。此外，这样的改动需要不同供应商之间进行大量的协调工作，以确保不同ECU之间可以互操作性，对于厂商是很难接受的。

    (2) 延迟和开销较大。虽然这些延迟可能对大多数通用操作系统是可以接受的，但是车辆操作有严格的实时约 束，较高的延迟和开销很难被接受。

## 六、车载网络攻防技术研究展望

    根据本文的总结, 车载网络的攻防研究面临如下几个挑战

    (1) 通用性和性能更强的车载网络协议逆向：当前的车载网络逆向技术存在通用性不足的问题，其适配的车型 有限。虽然一些工作在实验中可以取得较好的性能，但是其性能表现在不同车型上差别较大。此外，一些令牌解析的工作是半自动化的，需要专业人员介入，其自动化程度有待进一步提高。

    (2) 实时性更强的安全系统：汽车系统需要及时做出相应决策，因此ECU的实时性要求较高。一些安全攸关的 系统往往采用实时操作系统，但对于实时操作系统的攻防研究还相对较少。此外，一些ECU算力有限，因此无法部 署时延和开销较高的安全系统。

    (3) 向后兼容性的车载网络协议安全增强方案：很多车载网络协议安全增强工作需要对CAN等已经广泛部署的车载网络协议进行更改，这可能造成安全增强后的车载网络协议与旧款车辆的相关协议不兼容，不满足兼容性是很多安全方案在工业界无法大范围部署的重要原因之一。

    (4) 统一的车载网络安全测试标准和实验平台：虽然智能网联汽车在发售前都经过严格的网络安全测试，但目 前工业界还缺乏统一的车载网络检测标准。此外，当前的研究工作在实验平台、测试数据集和评估指标方面差别 较大，目前学术界缺乏统一的车载网络安全实验标准和平台。

    针对上述研究挑战，未来研究工作应关注以下方面：

    (1)多种方法融合并结合机器学习的车载网络逆向技术

    (2)针对车载网络ECU实时操作系统的攻击面分析和防御

    (3)多种方法结合的高实时性车载网络入侵检测方案

    (4)向后兼容的轻量级车载网络协议安全设计

    (5)统一的智能网联汽车的车载网络测试标准和实验平台

# 车载网络入侵检测技术综述

[原文PDF](./车载网络入侵检测技术综述_童一帆.pdf)

    智能网联车促进了交通运输的革新发展，但也伴生了网络安全问题。入侵检测技术作为一种轻量化的防御技术，可通过建立的特征对攻击进行有效检测。本文调研了近年来针对常见攻击所提出的入侵检测技术，并对这些技术的特征方法进行了划分。

**关键词：**入侵检测；车载网络；流量；负载；深度学习

## 一、车载网络架构概述

![image-20241029151356680](https://s2.loli.net/2024/10/29/ZnkS2KoOxyX6wTf.png)

    CAN由于其较低成本、较全工具链、一定的抗噪与容错性成为使用最广泛的车载网，尤其用于汽车动力系统、车身控制系统等。

![image-20241029151615056](https://s2.loli.net/2024/10/29/SjkNr5KTmJyhvX8.png)

## 二、车载网络攻击

    一般网络攻击分为两类：被动攻击和主动攻击。被动网络攻击（如窃听）主要违反目标系统安全的保密要求并导致隐私泄露（如位置信息、对话数据和摄像头记录等隐私数据）。主动网络攻击可以通过插入、删除或修改消息来阻碍系统功能。

**2.1 拒绝服务攻击**

    攻击者发送许多合法请求，超出服务系统的处理能力，致使系统资源耗尽而无法响应其他合理请求。

**2.2 消息注入和重放攻击**

    消息注入攻击是在网络中注入伪造的消息；重放攻击是将之前的消息重新注入到网络中。

**2.3 消息操纵**

    这种攻击通过更改/修改或删除消息来影响数据的完整性

**2.4 伪装攻击**

    攻击者先监视CAN总线以了解ECU A以什么频率发送了哪些消息，然后停止A的传输并利用ECU B代表A制造和注入消息。

**2.5 恶意软件攻击**

    攻击者将恶意软件利用通信接口的漏洞注入系统，从而将恶意消息发送到CAN总线上以实现消息注入攻击、重放攻击、DoS等特定的攻击

## 三、车载CAN网络IDS类型

    入侵检测依赖于观测的数据即车载网络中各节点之间交换的数据。消息的时间戳或者数据范围都可以作为特征成为区分消息是否正常的依据。一般可以将数据集的特征分为两种类型：物理特征和网络特征。物理特征是指系统物理状态的特征（如速度、发动机转速），而网络特征是指描述系统通信和数据方面的特征（如消息数量、数据序列）。

    通常将传统的IDS分为基于签名的IDS和基于异常的IDS。基于签名的IDS需要对已有攻击模式进行匹配，类似黑名单，误报率低但需要保持签名数据库最新，检测新攻击能力有限且对CPU、内存等资源要求较高。

    基于异常的IDS对正常的系统行为进行建模，当与正常系统行为偏差显著时视为入侵，该方法能够识别新型攻击，但容易产生误报，且正常系统行为的数据不易获得。

    近年，IDS可分为基于流量的IDS、基于负载的IDS和混合IDS。基于流量的IDS监控车辆的内部网络，从中提取不同的特征来识别入侵或异常行为；基于负载的IDS检查消息的负载以识别入侵；混合IDS是前两者组合

#### 3.1 基于流量的IDS技术

    基于流量的IDS技术可以有效识别特定数据包和频率的异常情况，对于传统CAN总线网络适用性更强同时实时性更好；但对于面向服务的车载网络，由于服务信号可根据服务需求进行变更，基于流量的IDS很难对新增的服务信号做出响应，也无法发现新增服务信号的篡改风险，所以该技术有其局限性。

#### 3.2 基于负载的IDS技术

    基于负载的IDS技术普遍引入机器学习机制完成正常样本的识别，该技术普适性较强。但存在机器学习的普遍问题，即正常样本和异常样本采集问题，特别是异常样本数量巨大，学习难度较高。因此，该技术如何获取大量样本进行学习是应用该技术的门槛。

#### 3.3 混合类型的IDS技术

    混合类型的IDS技术融合了基于流量的IDS和基于负载的IDS的优点，既能对选定的报文进行快速识别，同时又具备学习能力，可以学习新报文。但受限于车辆整体成本，IDS部署的控制器算力和存储空间普遍无法支撑混合类型的IDS技术，如何降低混合类型的IDS技术资源使用，是该技术能够广泛使用的前提条件。

## 四、结论

    入侵检测技术作为一种被动防御技术，具有低开销、应用广等特点。目前入侵检测技术主要分为基于流量的和基于负载的两大类，不同类型在成本开销、应用场景以及效果等方面具有较大差异，需根据实际情况设计入侵检测系统。

# 智能网联汽车车载CAN网络入侵检测方法综述

[原文PDF](./智能网联汽车车载CAN网络入侵检测方法综述_关宇昕.pdf)

    首先介绍了车载网络的安全属性，并分析了智能网联车的网络安全问题以及车载CAN网络的脆弱性和对其的攻击方式。其次总结了近几年车载CAN网络入侵检测方法的研究现状。最后对未来车载网络入侵检测系统发展提出几项开放性问题。

**关键词：**智能网联汽车；网络安全；车载CAN网络；异常行为；入侵检测系统

## 一、车载网络概述

#### 1.1 车载网络介绍

![image-20241029203037485](https://s2.loli.net/2024/10/29/TZjJ87HYV5pFlkP.png)

#### 1.2 车载网络的分类

![image-20241029203116364](https://s2.loli.net/2024/10/29/LBT5XWw4RFHtkpM.png)

![image-20241029203135089](https://s2.loli.net/2024/10/29/Eiz1LGsbB2N7qWj.png)

    CAN网络协议是一种串行数据通信协议，具有总线拓扑结构，CAN网络中的ECU节点均可向其他ECU发送报文。CAN网络具有非破坏性仲裁机制，当多个节点同时发送数据时，优先级由报文ID决定，ID越小优先级越高。

![image-20241029203411169](https://s2.loli.net/2024/10/29/6rBuZeR84MY9miX.png)

    LIN成本和网络安全威胁较低，常用于辅助CAN。主要应用于实时性不高的场合如雨刮器、车窗升降等部位。与CAN网络不同的是其结构是由一个主节点和一个或多个从节点组成，最多连接15个从节点。消息的时序由主节点决定，容错性较低。

    FlexRay是一种具备故障容错的高速车载网络。可通过单通道或双通道进行消息传输。主要应用在安全性极高的位置如电子制动、电子转向盘等。但由于其价格昂贵，不适合大量应用在车载网络中。

    MOST时一种用于汽车媒体系统中消息传输的车载网络，采用环形拓扑结构。采用塑料光纤作为物理层，将网络与电磁干扰隔离，防止信息娱乐系统中出现嗡嗡声等问题，比CAN更适合媒体系统数据传输。但由于成本高以及网关开发难度大，目前高端汽车应用较多。

    车载以太网的带宽比CAN网络协议的速度快约100倍，然后其成本远高于CAN。

## 二、ICV网络安全问题分析

#### 2.1 ICV的攻击途径分析

![image-20241029204348303](https://s2.loli.net/2024/10/29/1YRLvh2lUNX48pE.png)

#### 2.2 车载CAN网络脆弱性分析

    车载CAN网络在设计时存在的缺陷如下：

    仲裁机制的缺陷：CAN网络具有仲裁机制，网络中的节点通过报文ID来确定优先级。假如入侵者一直发送高优先级报文，导致CAN网络一直被占用，其他的节点无法发送报文。

    广播传输特性的缺陷：CAN报文以广播形式传输，网络中的所有ECU均可监听CAN网络中的消息。一旦黑客控制任意节点，就可通过该节点读取消息内容。

    缺少消息检验及认证机制：CAN网络缺乏身份认证机制，无法判断消息是否存在异常。当黑客破解CAN网络协议后，可直接向网络中发送伪造的报文。例如，高速行驶的汽车收到伪造的熄火命令， 但ECU无法识别消息的真伪，会导致车辆的突然熄火，引发交通事故。

    缺少信息安全及加密机制：CAN报文在CAN网中以明文形式传输。由于缺乏加密机制，黑客可以轻松读取并破解其中的数据。CAN网络中信息的完整性无法得到保障，存在信息泄露的风险。

#### 2.3 车载CAN网络攻击方式分析

![image-20241029204857639](https://s2.loli.net/2024/10/29/s2epiPTDlgxZKq7.png)

    嗅探攻击：当黑客成功入侵CAN网络后，可监听网络内部的报文并对其进行逆向工程，以便攻击车辆上的特定部件。

![image-20241029205257958](https://s2.loli.net/2024/10/29/1KjDr5Mb4Cfu6yO.png)

    DoS攻击：由于CAN网络的仲裁机制，黑客可向网络中发送大量高优先级的攻击报文，导致其它节点无法向网络中发送消息，严重的甚至可能导致车载网络的崩溃。

![image-20241029205307750](https://s2.loli.net/2024/10/29/T24McUeE1jRpgwk.png)

    重放攻击：当黑客捕获到ECU发送的报文后不对其做任何处理，再次将报文重放到网络中，可能导致车内正常通信受到干扰。

![image-20241029205317313](https://s2.loli.net/2024/10/29/QOm5fwdKZeWJrnT.png)

    篡改攻击：当黑客捕获到网络中的报文后，首先对报文的内容进行修改，再将其发送到CAN网络中。其中，修改的部位可能是报文ID或数据段的信息，以上两种篡改方式均会造成或多或少的影响。

![image-20241029205325533](https://s2.loli.net/2024/10/29/fcAIwpHbaeXrsuG.png)

    消息注入攻击：当黑客成功入侵CAN网络后，可直接向其内部注入恶意报文，可能会给汽车安全带来严重威胁。

![image-20241029205333584](https://s2.loli.net/2024/10/29/w9N7m8CBZIujMTt.png)

    欺骗攻击：当黑客掌握网络中CAN数据帧的详细信息后，便可将欺骗性的报文对网络实施特定的攻击。这些报文中包含错误的信息，可能会误导相应的ECU。

![image-20241029205344903](https://s2.loli.net/2024/10/29/PHdc9xANZKyz6Iq.png)

    丢弃攻击：当黑客成功入侵车载网络中的某一节点或者网关后，可以删除网络中的报文，导致某些重要的报文无法被其他节点接收，使汽车某些重要的功能出现异常。

![](https://s2.loli.net/2024/10/29/z14OiVNoAHxw2SG.png)

    模糊攻击：黑客使用某些变异算法将合法数据转换成随机数据，再将随机数据注入到CAN网络中，干扰车内正常通信。

![](https://s2.loli.net/2024/10/29/UCLDeoz5yta79sY.png)

    伪装攻击：黑客可以模拟节点向网络发送报文，由于CAN网络无消息认证机制，网络中的其他节点无法识别消息的真伪。

![](https://s2.loli.net/2024/10/29/IHh9iW7P8xsaCow.png)

## 三、车载网络入侵检测系统

    入侵检测按照检测技术分为基于签名的入侵检测系统和基于异常的入侵检测系统。基于签名的入侵检测系统通过监视预定义的攻击签名列表实现入侵检测。优点是出现假阳性概率低且速度快，但无法有效识别新型攻击，需要人工对数据库实时更新；基于异常的入侵检测系统通过监测车载网络状态是否偏离正常模式来识别入侵。优点是对未知攻击具有预测性。

#### 3.1 基于签名的车载CAN网络入侵检测方法

    虽然该方法对已知攻击有匹配速度快及高精度等优点，但对这种超大型数据库的维护也是一项挑战。可将该方法与基于异常的车载CAN网络IDS相结合来解决无法检测未知攻击的问题。

#### 3.2 基于异常的车载CAN网络入侵检测方法

    特征分为物理特征和数据特征，物理特征表示为车载网络通信在物理层存在的诸多规律（如电压波动、时钟偏移），而数据特征主要指传输报文的类别、标识、有效载荷、消息内容等。

![](https://s2.loli.net/2024/10/29/IPua9d2tQ4RvGUC.png)

**3.2.1 基于物理特征的方法**

![](https://s2.loli.net/2024/10/29/z51u6VUFmpAgT7n.png)

**3.2.2 基于信息论与统计的方法**

![](https://s2.loli.net/2024/10/29/UFM1aVd3lrwysYg.png)

**3.2.3 基于机器学习的方法**

![](https://s2.loli.net/2024/10/29/gKpWHPiDlQwMTrS.png)

## 四、车载网络入侵检测技术发展趋势

**4.1 如何提升车载网络IDS检测能力的全面性**

    现有研究多数针对车载CAN网络的一种或几种攻击方式进行入侵检测。不应仅局限于车载CAN网络单个方面实现入侵检测，也应考虑如何检测T-Box通信模块、V2X通信协议等或其他车载网络的入侵。

**4.2 如何构建基于车载网络IDS评估基准数据集**

    现多数研究采用KDD CUP和DARPA等数据集作为评估基准，未来如何统一测试数据集来标准化评估IDS检测性能有待解决。

**4.3 如何提升车载网络IDS的检测性能**

    检测性能包括检测精度、检测时间和检测系统的鲁棒性等。基于签名的车载网络IDS检测精度较高。基于机器学习的IDS方法可以检测未知攻击，但传统机器学习算法运算资料较高。应考虑如何提高检测算法计算速度、降低检测响应时间是目前待解决的问题。

# 基于深度学习的网络入侵检测系统综述

[原文PDF](./基于深度学习的网络入侵检测系统综述_邓淼磊.pdf)

    首先介绍了当前几种不同的入侵检测系统；接着介绍了基于深度学习的入侵检测系统中常用的数据集和评价指标；再总结了网络入侵检测系统中常用的深度学习模型及其应用场景；最后提出了当前研究所面临的问题及未来的发展方向。

**关键词：**网络安全；入侵检测；深度学习；异常检测；网络入侵检测系统

## 一、入侵检测系统的分类

![image-20241031111717016](https://s2.loli.net/2024/10/31/zqOufKxsBjFon6Z.png)

    本文针对网络入侵检测进行研究，组成部分如下图。

![image-20241031111832514](https://s2.loli.net/2024/10/31/RfbK87yVJj3UGIu.png)

    IDS组成部分如下：(1)网络检测：监控网络收集必要数据包，数据包由数据包头和数据包有效载荷组成，二者都可用于提取攻击所需信息。(2)数据收集：收集要进行攻击的目标系统的详细信息。(3)分析数据包细节：扫描网络数据包以窃取机密信息。(4)识别和存储签名/攻击模式：识别已知攻击和新型攻击的攻击模式，或识别可用于发起内部攻击的某些已知漏洞的签名。(5)生成警报：识别攻击模式后，生成警报给安全管理员。

#### 1.1 基于数据来源的分类

![image-20241031112604263](https://s2.loli.net/2024/10/31/x9XmSpU6GqiF4tY.png)

#### 1.2 基于检测技术的分类

![image-20241031112700767](https://s2.loli.net/2024/10/31/hiNbmxu7Q4CetUL.png)

## 二、数据集与评价指标

#### 2.1 数据集

    常用的主要有KDD99、NSL-KDD、UNSW-NBI5、CIC-IDS-2017等。

#### 2.2 评价指标

    真阳性TP：正确分类为攻击的攻击数据；假阳性FP：错误分类为攻击的正常数据

    真阴性TN：正确分类为正常的正常数据；假阴性FN：错误分类为正常的攻击数据

![image-20241031113117187](https://s2.loli.net/2024/10/31/Yc25xFqf1WPdB3h.png)

## 三、基于深度学习的入侵检测技术

    在基于深度学习的IDS中，深度神经网络可以自动降低网络流量的复杂度来发现数据之间的相关性，无需人工干预。故可以利用大量历史数据对深度学习模型进行训练，建立异常检测模型。

![image-20241031113849367](https://s2.loli.net/2024/10/31/7SvHTip6IPLtqrK.png)

#### 3.1 生成式架构

    生成式（或无监督）深度学习架构可以从无标签的原始数据中自动学习，可以检测与已知分布不一致的样本，识别出潜在的异常行为。

    (1)循环神经网络RNN：对序列的每个元素执行相同的任务，其输出取决于先前的计算，可以利用数据的序列信息提取时序特征，适合应用于与序列相关的入侵检测问题。长短期记忆LSTM和门控循环单元GRU是为了克服传统RNN在反向传播中面临的梯度消失或爆炸问题。

    (2)自编码器AE：通常用于通过产生比原始数据输入更好的数据表示来降维。AE将编码器和解码器结合在一起，并使用反向传播将它们训练在一起。编码器提取原始特征，并通过将输入转换为低维抽象来学习数据表示。然后，解码器接收低维表示并重建原始特征，自编码器主要用于数据的降维。

    (3)受限玻尔兹曼机RBM：原理是消除同一层神经元之间的联系。RBM能从原始数据中学习特征的深层次信息。

    (4)深度信念网络DBN：是一种具有深层架构的神经网络，由堆叠的RBM组成，通过无监督算法对每一层RBM进行训练，每个RBM都是在前一个RBM基础上训练的。

#### 3.2 判别式架构

    判别式（或监督）架构主要应用于标记数据以区分预测任务的模式。其通过学习从输入数据到标签的映射关系，即学习如何根据输入数据的特征对其进行分类。在入侵检测系统中，判别式方法能够从已知的数据样本中学习到正常和异常行为之间的差异，从而实现对未知数据的分类和判别。与生成式方法相比，判别式方法专注于学习数据的类别信息，不关注数据的潜在分布。

    卷积神经网络CNN是典型的判别式有监督方法，由输入层、卷积层、池化层、完全连接层和输出层组成，不同结构的CNN具有不同数量的卷积层和池化层。

#### 3.3 混合式架构

    混合式深度网络方法结合了生成式方法和判别式方法，主要有生成对抗式网络GAN和图神经网络GNN。

    GAN是一种混合深层架构，包含两个神经网络，生成器和判别器。GAN依赖于一个极小极大博弈，其中一个网络寻求最大函数值， 另一个网络试图最小化函数值。在每个对抗性回合中，生成器从噪 声中产生随机样本。然后鉴别器接收随机数据和实际样本，并试图 区分它们。通常情况下，网络中的异常流量远少于正常流量，GAN能 生成新数据，因此能用来解决入侵检测中数据类别不平衡的问题。

    深度学习（DL）在检测网络攻击方面能够从平面数据中学习可泛化模式。然而，平面数据无法捕获攻击的结构性行为。相反，图结构提供了一个更加健壮和抽象的系统视图。最近，图神经网络（GNN）成功地从图结构数据提供的语义中学习到有用的表示。因此GNN方法也被成功地应用于入侵检测中。

#### 3.4 不同类型入侵检测模型分析比较　

![image-20241031141321900](https://s2.loli.net/2024/10/31/z1aDbjwA2RLXQNE.png)

    (1)对于RNN，LSTM 和 GRU 成功克服了传统循环神经网络在训练过程中可能遭遇的“梯度消失或爆炸”问题。这一类模型的优势在于能够通过其特有的细胞结构来保持数据间的长期依赖关系。可以使用 RNN，LSTM 和 GRU 和其他神经网络组合构建入侵检测模型。

    (2)AE、DBM和DBN等深度学习技术在入侵检测系统中被广泛应用于特征提取和数据降维。这些方法通过学习数据的有效表示，能够从原始数据中提取出最具代表性的特征。在入侵检测系统中，这些深度学习技术通常与其他分类模型相结合，用于对输入数据进行预处理或特征提取。

    (3)采用卷积神经网络构建的入侵检测模型可以更好地提取数据中的空间特征，提高模型的计算效率。并且由于其权值共享的特性，能够有效减少所要训练的参数，降低了模型的自由度，避免了在有限的数据集上花费大量时间进行拟合所造成的过拟合。CNN的多层次特性使其不仅可以用于特征提取，而且在分类任务中也表现出色。其在入侵检测的分类任务中展现出高准确率，对网络流量数据的分析更加精确和全面。

    (4)生成对抗网络则被广泛应用于处理数据集不平衡的情况。通过生成更多的异常样本，GAN有助于平衡数据集中正常和异常样本的比例，减轻数据不平衡性带来的影响，提高模型的鲁棒性和泛化性能。

    (5)图神经网络凭借其出色的结构行为捕捉能力在入侵检测分类问题中表现卓越。对于涉及网络结构和节点关系的场景，GNN能够更好地理解网络流量的内在规律，进而提高分类准确性。

![image-20241031142156748](https://s2.loli.net/2024/10/31/mFtf98IiZYalrJy.png)

## 四、网络入侵检测系统的应用

**4.1 软件定义网络SDN**

**4.2 物联网IoT**

**4.3 车载网络IVN**

## 五、挑战与未来研究方向

    (1)误报率高的问题。

    (2)零日攻击指所有以前没有发现的新攻击。

    (3)高质量的数据集对于测试和验证提出的网络入侵检测系统至关重要。

    (4)实时检测问题。

    (5)数据集不平衡问题。

    (6)网络数据流量大和维度高的问题。

    (7)半监督学习 、迁移学习 、强化学习以及集成学习等方法在入侵检测系统方面尚未得到广泛的研究和评估。