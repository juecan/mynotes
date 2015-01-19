### RTP 及 RTCP 协议原理

#### 为什么用 RTP 传输媒体流，UDP 不够吗？

	VoIP 业务中的所有媒体流承载都用到了 RTP 协议

	基于 VoIP 的网络：
		移动网络中的 IMS、VoLTE
		2/3G 网络中的 Voice over CS
		微信、Skype 等互联网应用类 VoIP
		Avaya、Cisco 为大企业客户提供的语音解决方案（如 Call Manager 等）
		
	媒体流（语音、视频等多媒体流量）的传输协议一定是 RTP
	
	VoIP 业务中的媒体流传输的通用协议栈：
		RTP：Real Time Transport Protocol
		RTCP：RTP 控制协议
		传输层由 UDP 承载
		
	使用 UDP：
		传输层是为上层用户服务
		媒体流对延迟敏感
		TCP 确认、重传机制复杂
		UDP 相对简单
		
	为何光有 UDP 不够，还需要 RTP：
		传输媒体流对网络的要求：IP 网络的不可预知性，数据包可能存在丢失、错序等问题
		因此，接收端需要能正确还原音频或视频信号，需要：
			1. 检测出错序，并保持采样和播放之间的同步关系（解决方案：时间戳）
			2. 需要在接收端能够检测出分组丢失（解决方案：序列号）
		那就只有用 RTP 了，UDP 没这功能
