## IMS 网络概述

### IMS 的产生背景以及 IMS 是什么？

	业务域：语音（CS，Circuit Switch）、数据（PS，Packet Switch）
		业务：网元 -> 网络
		固网语音业务：PSTN 交换机 -> PSTN 网络
		移动传统语音业务：MSC-S、媒体网关、GMSC、智能网、短信中心 -> GSM 网络、3G 网络（WCDMA、TDSCDMA）
		本身并不提供语音业务，仅提供数据业务（VoIP、VoLTE）：MME、SGW、PGW -> 4G LET 网络
		微信、Skype、微博等互联网服务：骨干路由器、汇聚路由器、接入路由器、防火墙 -> 数据网络（固网）

	问题：
		垂直建设的网络（都是语音业务，要重复部署多套）
		封闭的网络（开发一个群聊功能要半年？）
		业务重叠的网络
		难以维护的网络（2000 台 MSC-S、1000 台媒体网关要做补丁升级修复 BUG）
		维护成本高的网络（都是语音业务，要养几套不同的维护人员）
		
	IMS：IP Multimedia Subsystem，IP 多媒体子系统
		基于 IP 的传输
		基于 IP 的会话控制
		基于 IP 的业务实现
		
		语音、视频、图片、文本等多种媒体的组合
		支持多种接入方式，各种不同能力终端
		
		依赖于现有网络技术和设备，最大程度重用现有网络系统
		无线网络把 PS/GPRS 网络作为承载网络
		固定网络把基于固定接入 IP 系统作为承载网络
		
		有 3GPP 在 R5 阶段（2005）引入，叠加在 PS 域上，目的是在基于全 IP 的网络上为移动用户提供多媒体业务
		
		与接入无关
		
		         |---> Fixed -> PSTN/固网(ADSL)/有线网络(Cable)/WLAN
		IMS ---> |
		         |---> Mobile -> WLAN/WMAX/GSM/3G/2.5G(UMTS)/4G(LET)

	端到端的全 IP 化是网络发展趋势，4G 的 LTE 本身就是一张全 IP 的网络
	
	Mobile Phone/PC
	Any IP connection(e.g. CDMA, GPRS, EDGE, WCDMA, LTE, WLAN, WiMAX, ADSL) <---> User plane connection <---> IP based Services possible between terminals
	
	33:00