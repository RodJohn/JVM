# CMSGC时间过长


## 情况一 ：ReScan时间过长

示例

	[Rescan (parallel) , 0.6762340 secs]

分析

	ReScan扫描时间过长，应该是新生代过多

处理

	
	开启Remark前强制YGC（-XX:+CMSScavengeBeforeRemark）

## SWAP 区域 

前提是你的服务器上是有 SWAP 区域（用 top、 vmstat 等命令可以看出）用于内存的换入换出，那么操作系统可能会将 JVM 中不活跃的内存页换到 SWAP 区域用以释放内存给线程使用（这也透露出内存开始不够用了）。内存换入换出是一个开销巨大的磁盘操作，比内存访问慢好几个数量级。

再看看此时的 vmstat 命令中 si、so 列的数值，如果数值大说明换入换出严重，这是内存不足的表现。

解决方法：减少线程，这样可以降低内存换入换出；增加内存；如果是 JVM 内存设置过大导致线程所用内存不足，则适当调低 -Xmx 和 -Xms。



