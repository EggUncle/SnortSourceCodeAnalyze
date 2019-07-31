# Snort介绍
在介绍snort之前，先简单的介绍一下，IDS和IPS
## IDS&IPS
这一部分是网上摘录的
### IDS
>IDS是英文“Intrusion Detection Systems”的缩写，中文意思是“入侵检测系统”。专业上讲就是依照一定的安全策略，通过软、硬件，对网络、系统的运行状况进行监视，尽可能发现各种攻击企图、攻击行为或者攻击结果，以保证网络系统资源的机密性、完整性和可用性。做一个形象的比喻：假如防火墙是一幢大楼的门锁，那么IDS就是这幢大楼里的监视系统。一旦小偷爬窗进入大楼，或内部人员有越界行为，只有实时监视系统才能发现情况并发出警告。
### IPS
>入侵防御系统(IPS: Intrusion Prevention System)是电脑网络安全设施，是对防病毒软件（Antivirus Programs）和防火墙(Packet Filter, Application Gateway)的解释。 入侵防御系统(Intrusion-prevention system)是一部能够监视网络或网络设备的网络资料传输行为的计算机网络安全设备，能够即时的中断、调整或隔离一些不正常或是具有伤害性的网络资料传输行为。
### IDS和IPS的区别
>IPS对于初始者来说，是位于防火墙和网络的设备之间的设备。这样，如果检测到攻击，IPS会在这种攻击扩散到网络的其它地方之前阻止这个恶意的通信。而IDS只是存在于网络之外起到报警的作用，而不是在你的网络前面起到防御的作用

## Snort
接下来简单介绍一下snort和它所使用的规则。

关于用法和各个模块介绍的详细信息，可以参考：
1. 官方文档：https://snort.org/downloads/snortplus/snort_manual.pdf
2. github：https://github.com/snort3/snort3

>Snort是一个免费的、开源的网络入侵防御和检测系统。它使用基于规则的语言，执行协议分析、内容搜索/匹配，并可用于检测各种攻击和探测，如缓冲区溢出、隐形端口扫描、CGI攻击、SMB探测、操作系统指纹识别尝试等。

### Snort 规则介绍
#### 1.文本规则
这种规则比较简单，主要就是由snort的规则语法组成，主要包括规则头和规则选项。

规则头主要标明以下几点：
- 动作类型（例如alert为输出告警）
- 协议类型（tcp/udp/ip/icmp）
- 源ip
- 源端口
- 方向 ( -> / <- / <> )
- 目的ip
- 目的端口

规则选项涉及到的类型就比较多了，这里仅列出一小部分，详细的规则信息以及用法请参考官方文档
- msg (告警时输出的信息)
- flags (tcp的flag，例如ack，syn等)
- gid 规则所属的组的id
- sid 规则所属的id
- rev 规则版本
- content 用于匹配数据包内容
- dsize 数据包大小

这里举一个简单的例子，如果现在需要在捕获任意源ip端口到任意目的ip端口的tcp的ack包时输出告警信息"tcp ack packet",那么规则可以这样写
```
alert tcp any any -> any any (msg:"tcp ack packet";flags:A;)
```

#### 2. build in规则
这类规则比上一类的规则要更加简单，它们的检测逻辑都已经预置在snort中了，有些需要进行一定配置。这里以端口扫描检测举例，这里摘录上面提到的官方文档中```9.29 port_scan```的一小部分
```
• 122:1 (port_scan) TCP portscan
• 122:2 (port_scan) TCP decoy portscan
• 122:3 (port_scan) TCP portsweep
• 122:4 (port_scan) TCP distributed portscan
```
如果说要检测tcp的端口扫描，那么根据build in规则，就比较好写了。
```
alert ( msg:"tcp portscan";gid:122;sid:1;rev:1;)
```
这里仅需要在规则中写上对应build in规则的gid和sid，就可以检测了。
