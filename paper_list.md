# 看过的论文列表

格式 ： 标题 会议 年份 (谷歌学术链接)  论文motivation逻辑链条->方法（一句话概括idea)  

## 网络系统设计

[SONIC: Application-aware Data Passing for Chained Serverless Applications. ATC 2021](https://www.usenix.org/conference/atc21/presentation/mahgoub) 这篇文章从链式的serverless应用所需的传输中间层数据开销（spark计算流图传输中间计算结果）为出发点，讨论了现有的三种解决方案 VM-Storage(同一虚拟机上服务），Directly Pass(不同虚拟机但是同一物理节点）remote storage（不同物理节点）的不足，指出现有的三种方案无法应对所有的应用需求。基于此提出了SONIC,这是上述三种方案的混合方案，对DAG上任意一条边（数据流动）能够根据应用的需求选择合适的技术方案。 ps：可以用来启发以后two-stack bypass等技术方案的设计。

Live in the Express Lane (ATC 2021) 大部分的分布式应用利用节点之间弱同步的方式来应对底层基础设施的不确定性。这种同步依赖于节点之间的有界传输延迟（bounded-latency)。如果能确保节点之间具有极低的交互延迟，并且抖动是有界(bounded)，将大大提升分布式应用的性能。特别是对于分布式应用里的协调模块, 例如 zookeeper。（背景）但是目前的数据中心底层基础设施无法提供这种有界低延迟。因为目前数据中心底层基础设施主要由商用硬件(通用多核CPU)和软件(Linux内核)组成。在商用软硬件上并发执行的事务会对传输延迟造成无法预测的干扰。在该paper之前很多工作聚焦于低传输延迟，但并不能保证有界的抖动（bounded jitter)，无法消除商用软硬件对传输延迟带来的干扰。（挑战) 为了解决以上挑战，该论文提出了Express-Lane（X-lane)。X-lane 提供了个位数微秒级的传输延迟和纳秒级的有抖动，为分布式应用提供了无干扰的通信环境。(design)X-lane的设计由两部分组成。1. 通信模型的设计（即协议的设计), 设计了periodical 传输协议，以及packet级别的流量工程来减少丢包，降低排队延迟。2. 消除通用软硬件(多核CPU和Linux内核）抖动源（内核细节，关闭中断，重定向中断，关闭watchdog等）。
