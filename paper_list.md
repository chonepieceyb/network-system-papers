# 看过的论文列表

格式 ： 标题 会议 年份 (谷歌学术链接)  论文motivation逻辑链条->方法（一句话概括idea)  

## 网络系统设计

[SONIC: Application-aware Data Passing for Chained Serverless Applications. ATC 2021](https://www.usenix.org/conference/atc21/presentation/mahgoub) 这篇文章从链式的serverless应用所需的传输中间层数据开销（spark计算流图传输中间计算结果）为出发点，讨论了现有的三种解决方案 VM-Storage(同一虚拟机上服务），Directly Pass(不同虚拟机但是同一物理节点）remote storage（不同物理节点）的不足，指出现有的三种方案无法应对所有的应用需求。基于此提出了SONIC,这是上述三种方案的混合方案，对DAG上任意一条边（数据流动）能够根据应用的需求选择合适的技术方案。 ps：可以用来启发以后two-stack bypass等技术方案的设计。
