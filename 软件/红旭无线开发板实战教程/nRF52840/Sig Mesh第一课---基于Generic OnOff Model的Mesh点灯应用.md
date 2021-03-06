## 前言
> 该文字教程主要是讲解如何通过Nordic官方的Mesh SDK包,创建一个标准的Generic OnOff模型.目前网络上对于关于SIG MESH相关的实战文字教程很少,截至目前小编写这篇文章时还未发现有任何实战的文字教程.更多的是SIG MESH前景、概念以及跟其他的无线通讯技术的对比.其实，这些概念SIG MESH的spec都有说明的.因些,小编可以毫不客气地说我们红旭应该是全网首发.

## 背景
众所周知,2017年7月19日, 蓝牙技术联盟正式宣布，蓝牙（Bluetooth®）技术开始全面支持Mesh网状网络。全新的Mesh功能提供多对多设备传输，并特别提高构建大范围网络覆盖的通信效能，适用于楼宇自动化、无线传感器网络等需要让数以万计个设备在可靠、安全的环境下传输的物联网解决方案。这给予了Zigbee很大的震撼,搞不好分分钟就要交出"组网霸主"的位置.**就连小米这样的公司现在都对zigbee不太感兴趣了,对BLE MESH蠢蠢欲试(这话是从小米生态链公司的员工听来的)**.网络上也充斥着大量的众说纷纭的文章,在小编看来只不过代表各方面利益罢了.小编跟很多搞技术的工程师一样,物联网如果协议没有办法做到大部分统一,就不可能有独角兽出现.未来的趋势更多的是**"多线并存,多线合一"**的局面.

## 基础知识
毕竟SIG MESH是一个比较新鲜的事物,想要创建一个标准的SIG Model还是要有基础理论知识做支撑.不然一切都是空谈,在这里小编再次强调一遍,小编特别反感以下这几种情况:
- 一些工程师啥也不看也不管,一上来就直接看源码,直接一个<code>F5</code>编译烧录固件至开发板上.然后,看到现象效果出来了就好开心.最后就拔电源线了.
- 一些工程师基础的概念都没有搞明白,一上来直接就问我要怎么组网,我要怎么去点亮那盏灯

对于这样的工程师,真的是又恨又好笑.就算想要教,起码自身也要先看看相关的资料理清之间的关系吧.遇到这样的事情,小编大多数是这样的表情:
![](https://raw.githubusercontent.com/xiaolongba/picture/master/%E6%88%91TM....jpg)

### 模型
在BLE MESH网络中,节点与节点之间的信息传递都是通过模型去实现的.比如万年不变的"点灯模型"、"查水表模型"以及"各种传感器模型"等等.那么,有人就会说了小编你特么装逼都装了三个章节了,我们也忍了你三个章节了.赶紧出干货,别BB．好的，小编就大声地告诉你什么是模型．正所谓，一图胜千言，各位大佬请看图：

![](https://raw.githubusercontent.com/xiaolongba/picture/master/%E6%A8%A1%E5%9E%8B.png)

#### Configuration Server model
这个模型是强制的,存在于所有的Mesh设备中且仅存在于首个元素中即**Primary Element**.其作用主要表示一个设备的Mesh网络配置,类似于存储了节点的Mesh网络配置.而其对应的一个**Configuration Client model**,则可以设置并读取对端设备的**Configuration Server model**的内容.

#### Health Server Model
这个模型不是强制的是可选的,可以存在于不同的元素中.但是,一个元素中只能存在于一个这样的模型.其作用主要用于表示设备的Mesh网络诊断.而其对应的一个**Health Client Model**,则可以设置并读取对端设备的**Health Server model**的内容.

#### Generic OnOff Server
这个模型是标准的通用开关服务,常用于只需二值信号的,比如"开关灯"、"开关插座"等应用场景.而其对应的一个**Generic OnOff Client**,则可以设置并读取对端设备的**Generic OnOff Server**的内容.

#### Vendor Model Server
这个蓝牙技术联盟提供的一个自定义模型,常用于标准中没有的模型等应用场景.因为社会是不断地发展的,谁都无法预料以后又会出来什么高科技产品,就像Zigbee的ZCL在制定之初,谁知道会有智能锁这玩意呢?但是,我仍然希望尽可能的用标准的模型.而不是私有的模型,只有标准一统,物联网天下才能统一,工程师才有价值.否则,因为协议无法统一导致这门技术最终没人用或者被另外的新技术替换,这就有点得不偿失了.

### 内容未完
更多的详细内容,请关注我们的QQ群671139854,具体如下所示:

![QQ群](https://raw.githubusercontent.com/xiaolongba/picture/master/QQ%20Group.jpg)
