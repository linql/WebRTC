# EasyRTC

一个出色的开源WebRTC套件。

这个套件基于HTML5和JavaScript实现，包含了EasyRTC服务器的安装和客户端API，运行于Node环境，支持在线多人视频，语音，文本信息发送等功能。


## <a name='toc'>目录</a>


1. [什么是EasyRTC OpenSource](#What-Is-EasyRTC-OpenSource)
2. [特征](#Features)
3. [EasyRTC Open Source应用架构图](#Application-Architecture-Diagram)
4. [安装](#install)
5. [有用的术语](#Useful-Terminology)


## <a name='What-Is-EasyRTC-OpenSource'>一、什么是EasyRTC OpenSource</a>

EasyRTC OpenSource是：

- 用JavaScript编写的浏览器客户端库。 该客户端处理信令，并在很大程度上将应用程序与WebRTC API中正在进行的更改隔离。
- 基于Node.js的信令服务器。Node.js可以运行在单核心Raspberry Pi（第一版）的云服务器上。

总之，这两个组件可以让你用几行简单的代码编写一个简单的视频会议应用程序或文件共享应用程序等等。

## <a name='Features'>二、特征</a>

EasyRTC消除了开始使用WebRTC的痛苦，其有以下很酷的特征：

1. 跨浏览器支持。
2. 源代码执行。
3. 轻松安装服务器。EasyRTC服务器基于Node.js编写，它可以让你的应用程序运行于自己的机器或云服务器上，在Linux、Windows、或Mac系统上安装只需几分钟。使用EasyRTC的JavaScript客户端SDK可以让你快速的构建和部署WebRTC应用。
4. 使用WebSocket服务。
5. 服务器和客户端的单一语言（JavaScript）。EasyRTC 代码示例有助于缩短学习曲线，并让你快速掌握WebRTC的应用。
6. 免费开放源码。EasyRTC在BSD 2开源许可协议下运作，这意味着它的源代码是完全免费开放的，不用支付任何费用或其他隐藏费用。

## <a name='Application-Architecture-Diagram'>三、EasyRTC Open Source应用架构图</a>

![应用架构图](./images/Architecture-Diagram.png)


## <a name='install'>四、安装</a>

安装一个EasyRTC服务器到你的工作站中（无论是台式机或笔记本电脑）是非常快速和简便的。在同一工作站中运行EasyRTC客户端也无需使用繁琐的SSL证书。这对于测试你的客户端应用程序和其他设备一起运行情况将是非常有用的；而运行在Chrome浏览器中的 WebRTC客户端是不能访问摄像头或麦克风的，除非它们是架构在SSL服务器或在同一台机器上（这是浏览器的安全约束）。

#### 安装EasyRTC

1. 安装最新版本的[Node.js](https://nodejs.org/)(若已安装，略过此步骤)：

   ```shell
   [root@localhost src]# wget https://nodejs.org/dist/v8.7.0/node-v8.7.0.tar.gz
   [root@localhost src]# tar -zxvf node-v8.7.0.tar.gz
   [root@localhost src]# cd node-v8.7.0
   [root@localhost node-v8.7.0]# ./configure
   [root@localhost node-v8.7.0]# make
   [root@localhost node-v8.7.0]# make install
   [root@localhost node-v8.7.0]# ln -fs /usr/local/bin/node /sbin/node #让所有用户都可用node
   [root@localhost node-v8.7.0]# node -v #测试node是否安装成功
   ```

2. 安装[Git](https://git-scm.com/downloads)客户端(若已安装，略过此步骤)：

   ```shell
   [root@localhost src]# yum install git
   [root@localhost src]# git --version  #测试git是否安装成功
   ```

   或通过编译安装：

   ```shell
   [root@localhost src]# wget https://git-core.googlecode.com/files/git-1.9.0.tar.gz
   [root@localhost src]# tar -zxvf git-1.9.0.tar.gz
   [root@localhost src]# cd git-1.9.0
   [root@localhost git-1.9.0]# ./configure --prefix=/usr/local/git
   [root@localhost git-1.9.0]# make
   [root@localhost git-1.9.0]# make install
   [root@localhost git-1.9.0]# git --version  #测试git是否安装成功
   ```

   添加git到环境变量：

   ```shell
   [root@localhost src]# vi /etc/profile
   ```

   将其打开把：

   ```shell
   export PATH=$PATH:/usr/local/git/bin:/usr/local/git/libexec/git-core
   ```

   这句放在“export PATH USER LOGNAME MAIL HOSTNAME HISTSIZE INPUTRC”的上一行。
   （因为bin目录只有4个命令，其它的几十个命令在libexec/git-core目录下，所以，在PATH搜索路径下，也要加上才能找到）
   立即生效环境配置，不需要重启，用下命令：

   ```shell
   [root@localhost src]# . /etc/profile
   ```

3. 从GitHub库获取 EasyRTC源码并安装项目依赖：

```shell
[root@localhost src]# git clone git@github.com:priologic/easyrtc.git
[root@localhost src]# cd easyrtc
[root@localhost easyrtc]# cnpm install
```
4. 安装server_example的项目依赖：

```shell
[root@localhost easyrtc]# cd server_example
[root@localhost server_example]# cnpm install
```

5. 如果你没有看到任何令人讨厌的错误，那么你应该能够通过下面的命令来启动EasyRTC服务器（在server_example目录中）：

```shell
[root@localhost server_example]# node server.js
```

​	默认情况下，服务器提供演示应用程序的端口为8080，所以如果你在同一台机器上打开一个兼容WebRTC的浏览器，并打开http://localhost:8080，它将把带到一个demo汇总页面。选择一个demo（简单的音频视频demo是一个不错的选择）。打开一个新的页签并打开同一个URL以获得demo的第二个实例，您就可以尝试双向通信了。

​	警告：如果你在同一个没有耳麦的实体房间运行相同的两个WebRTC应用实例，它们会向彼此输出音频，导致产生一个尖锐的回音。如果有人在这房间里头，建议先将扬声器静音。 

​	注意：Simple Video+Audio Demo显示本地摄像机的输出（这是一个很好的提醒，所以你不会在会议中做任何粗鲁的事情）和潜在的远程摄像机的输出。 当你在同一台机器上运行所有的东西时，你会注意到一个显示是相对于另一个显示的(即镜像显示的)。 如果您想知道为什么这样做，请尝试以下操作：

- 在摄像头前面抬起左手，并考虑哪个视频窗格看起来是正确的。
- 在摄像头前面保留一些打印的文本，并考虑哪个视频窗格看起来是正确的。

## <a name='Useful-Terminology'>五、有用的术语</a>

- Video track（视频轨道）：表示单个视频或等效设备输出的对象
- Audio track（音频轨道）：表示单个麦克风或同等设备输出的对象

- Media Stream（媒体流）：用作包含一个或多个视频轨道和/或一个或多个音频轨道的对象。

- Data channel（数据通道）：用于将字符串或二进制数据从一个点发送到另一个点的对象。即在两者之间建立了一个双向数据通道的连接，实现点对点通信。

- Peer connection（对等连接）：作为两个点之间连接的对象，允许在网络上共享媒体流和数据通道。

- Easyrtcid：EasyRTC服务器上某个peer的唯一ID。

- Call（呼叫）：作为动词，表示与另一个点建立连接的行为，以便媒体流或数据可以被发送。 作为名词，表示有一个点对点连接的状态。