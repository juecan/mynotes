### GSM 网络中短消息业务的发送，背后都发生了什么？

	大家都感觉到，发送短消息已经成为日常生活必不可少的一部分，其实短消息服务并没有想象中的复杂，既然不难，为什么我们不来花几分钟时间了解下短消息的具体发送过程呢？
	故事开始时，我们看到我们的工作人员正在发送短消息，当他编辑好文字，按下发送键，短消息就开始了一段奇妙又去的旅程。
	
	当短消息离开了我们的手机，它通过空中接口传送到最近的无线网络节点 BTS（基站）；
	
	当短消息被 BTS 接收后，将由 BTS 通过 Abis 接口转发给所属的 BSC（基站控制器）；
		BSC 负责的功能包括分配无线信道、负责信令在不同的小区间迁移；
		BSC 的另一个功能是汇聚接收到的流量，从而减少进入上级网络的流量；
		
	当消息离开了 BSC，它将通过 A 接口发送给网络的心脏——MSC；
	
	MSC 收到后，该消息将存储在 SMSC，用户的详细信息将通过以下两个数据库进行验证；
		VLR，可以看做是主数据库 HLR 的一份拷贝，包含了 IMSI、MSISDN 以及用户使用短消息业务的详细信息；
		MSC 接下来将查询 EIR 数据库，来确认用户手机是否被盗或克隆；
		
	当信息被确认之后，我们的短消息将踏上这段旅程的最终归途；
	
	MSC 接下来通过保存在消息中的电话号码查询 HLR，获取为接收者服务的 Serving-MSC 所在的信息；
	
	接下来，消息将路由给 S-MSC，S-MSC 接收到消息之后，S-MSC 将消息发送给离接收者最近的 BSS（BSC+BTS）；
	
	最后由 BSS 将消息转发给最终的接收者。
	
	Mobile Phone -> The Air Interface - BTS(The Base Tranciever Station (Cell))
	-> The ABIS Interface -> BSC(The Base Station Controller)
	-> The "A" Interface -> MSC(The Mobile Switching Centre)
	-> SMSC(The short Messaging Service)
		-> VLR(The Visitors Location Register)
			-> HLR(The Home Location Register, The networks main subscriber database)
		-> EIR(The Equipment Identity Register)
	-> MSC(The "Serving" MSC, contains the recipients current location)
		The MSC connects to the nearest BSS in range of the recipients mobile phone and forwards the message to its destination.
	-> The "A" Interface -> BSC
	-> The ABIS Interface -> BTS
	-> The Air Interface -> Mobile Phone
	
### 专业词汇

	BTS：Base Transceiver Station，基站收发信台
		是 GSM/GPRS/EDGE 网络的 RAN(Radio Access Network，无线接入网)网元
		是负责一个小区(Cell)无线信号收发的设备的集合。这些无线设备包括天线、TRX(Transceiver，收发信机)、合路/分路器等。
		BTS 通过 Um 接口(GSM/GPRS/EDGE 网络的空中接口)与 MS(Mobile Station，移动台)通信，通过 A-bis 接口与 BSC 通信。
		一组 BTS 可以由一个 BSC 控制。
		
	Abis：基站子系统的两个功能实体 BSC（基站控制器）和 BTS（基站收发信台）之间的通信接口，用于 BTS 与 BSC 之间的远端互连方式
		该接口支持所有向用户提供的服务，并支持对 BTS 无线设备的控制和无线频率的分配。
		该接口是非完全开放的接口。
		其物理连接通过 2Mb/s 数据/链路实现
		信号方式也采用开放互连结构，其第一、第二、第三层接口协议分别满足GSM建议书08.54、08.56、08.58的要求。
		Abis 接口为私有接口，即 BTS 和 BSC 的协议可以根据各设备商自行规定。
		Abis 接口采用语音压缩技术，并通过信道复用，使传输一路语音只需要 9.6K 的带宽，远小于标准的脉码调制 64K，亦小于 GSM 中的 14K，故一路 2M 链路可支持 200 多路语音，而非传统技术的 30 路。
		通常情况下，如果是用来进行临时性的通信支撑，只需要开通 2 路 2M 链路即可保障通信要求。
		OpenBSC 是一个开源的基站控制器（Base Station Controller）

	BSC：Base Station Controller，基站控制器。由以下模块组成：
	　　AM/CM 模块：话路交换和信息交换的中心。
	　　BM 模块：完成呼叫处理、信令处理、无线资源管理、无线链路的管理和电路维护功能。
	　　TCSM 模块：完成复用解复用及码变换功能。
	
		BSC 控制一组基站，其任务是管理无线网络，即管理无线小区及其无线信道，无线设备的操作和维护，移动台的业务过程，并提供基站至MSC之间的接口。将有关无线控制的功能尽量的集中到BSC上来，以简化基站的设备。
		
	MSC：Mobile Switching Center，移动交换中心
		2G 通信系统的核心网元之一。
		是在电话和数据系统之间提供呼叫转换服务和呼叫控制的地方。
		MSC 转换所有的在移动电话和 PSTN 和其他移动电话之间的呼叫。
		移动网络完成呼叫连接、过区切换控制、无线信道管理等功能的设备，同时也是移动网与公用电话交换网(PSTN)、综合业务数字网(ISDN)等固定网的接口设备。
		MSC 是整个 GSM 网络的核心，它控制所有 BSC 的业务，提供交换功能及和系统内其它功能的连接，MSC 可以直接提供或通过移动网关 GMSC 提供和公共交换电话网（PSTN）、综合业务数字网（ISDN）、公共数据网（PDN）等固定网的接口功能，把移动用户与移动用户、移动用户和固定网用户互相连接起来。
		MSC 从 GSM 系统内的三个数据库，即归属位置寄存器（HLR）、拜访位置寄存器（VLR）和鉴权中心（AUC）中获取用户位置登记和呼叫请求所需的全部数据。
		另外，MSC 也根据最新获取的信息请求更新数据库的部分数据。
		作为 GSM 网络的核心，MSC 还支持位置登记、越区切换、自动漫游等具有移动特征的功能及其它网络功能。
		对于容量比较大的移动通信网，一个 NSS（网络子系统）可包括若干个 MSC、HLR 和 VLR。当某移动用户A进入到一个拜访移动交换中心（VMSC），为了建立对该移动用户 A 的呼叫，要通过移动用户A所归属的 HLR（归属位置寄存器）获取路由信息。
		
		在 GSM 网络中最重要的节点是 MSC，它负责控制由手机发起或终止的用户呼叫。
		
		Mobile-services Switching Center，移动业务交换中心
		
	VLR：Visitor Location Register，拜访位置寄存器
		它是一个动态数据库，存储所管辖区域中 MS（统称拜访客户）的来话、去话呼叫所需检索的信息以及用户签约业务和附加业务的信息，例如客户的号码，所处位置区域的识别，向客户提供的服务等参数。
		在网络中 VLR 都是与 MSCS 合设，协助 MSCS 记录当前覆盖区域内的所有移动用户的相关信息。
		
		在所有用户相关的信息中，其位置信息是一个动态值，也被记录在 VLR 中。
		说到移动网络的位置信息，先介绍一下位置区标识 LAI（Location Area Identity）的概念，位置区 LA 是移动系统中一组小区（Cell）或服务区（SAC）的集合，每个 MSCS 会管理数个位置区，VLR 则服务于一个 MSCS，帮助其记录管辖区域内所有活动用户的位置信息，当然位置信息只是 VLR 记录的众多用户相关信息中的一项。
		
	HLR：Home Location Register，归属位置寄存器
		它是一个负责移动用户管理的数据库，永久存储和记录所辖区域内用户的签约数据，并动态地更新用户的位置信息，以便在呼叫业务中提供被呼叫用户的网络路由。
		大致的呼叫流程：每当某用户做被叫时，主叫的 MSCS 会发送消息给 HLR 网元请求路由信息，HLR 查找数据库记录，向被叫用户当前所在的 MSCS/VLR 请求一个漫游号码，并将此号码发送给主叫 MSCS，主被叫 MSCS 之间通过该漫游号码找到对方，并最终建立起主被叫用户之间的通话。
		
	EIR：Equipment Identity Register，设备标识寄存器
		手机用户发起呼叫，移动交换中心（MSC）和拜访位置寄存器（VLR）向移动台（手机）请求 IMEI，并把它发送给 EIR，EIR 将收到的 IMEI 与白、黑、灰三种表进行比较，把结果发送给 MSC/VLR，以便 MSC/VLR 决定是否允许该移动台设备进入网络。
		因此如果该移动台使用的是偷来的手机或者有故障未经型号认证的移动设备，那么 MSC/VLR 将据此确定被盗移动台的位置并将其阻断，对故障移动台也能采取及时的防范措施。
		通常所说的通过网络追踪器追踪被盗手机就是通过 EIR 实现的。
		EIR 通过检查手机的 IMEI（International Mobile Equipment Identity，国际移动设备标识）来防范手机被盗从而保障系统的安全性
	