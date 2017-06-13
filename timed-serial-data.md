#基于Lambda架构的时间序列大数据分析
---

在金融分析领域一般根据数据的实时性及时效性采用不同的数据分析技术，如下图，对于实时性高的热数据采用实时流处理技术，可供选择的数据处理技术如Storm、CEP等。


对于次冷数据或冷数据的批量数据一般采用MapReduce和分布式并行处理架构。但是，越来越多的需求要求应用架构能够同时支撑实时数据和批量数据。这样，Lambda架构就应运而生了。

Lambda是由Storm的作者Nathan Marz在2014年的一篇论文中最先提出，最近逐渐得到业内认可。Lambda架构的目标是设计出一个能满足实时大数据系统关键特性的架构，包括有：高容错、低延时和可扩展等。Lambda架构整合离线计算和实时计算，融合不可变性（Immunability），读写分离和复杂性隔离等一系列架构原则，可集成Hadoop，Kafka，Storm，Spark，Hbase等各类大数据组件，下图是经典的Lambda架构的逻辑视图：

Lambda架构的主要思想就是将大数据系统构建为Speed layer、Serving Layer、Batch Layer分别对应于架构图中不同的视图View，在Speed layer，增量实时数据到Server layer的Real-time view中，可以直接被查询。在Batch layer，会有Batch Recompute对批量数据进行聚合、分类计算，计算结果到Precompute view中，然后传到Server layer的batch view中，Batch Viwe中的数据和Real-time View中的数据可以被Merge查询。 

Lambda架构在交易中心的一个典型应用场景就是本币监测系统或统一交易监测平台的设计。在本币监测系统中，既有根据数据流计算时间窗口内的异常交易的要求，也有根据历史数据进行防欺诈的要求。现有的技术很难将数据的实时性和大数据分析完美的结合在一起。

而利用lambda架构则可以很好地适应这一要求。我们在lambda架构的基础上，做了原型实验，取得了不错的效果。

	