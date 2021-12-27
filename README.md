# 
Make TiDB on cloud more native and nb native .
# 作者
- [mikechengwei](https://github.com/mikechengwei)
- [caohe](https://github.com/caohe)
- [devenzhou](https://github.com/devenzhou)
- [tomatopunk](https://github.com/tomatopunk)

# 项目介绍
解决当前TiDB在云上云原生方式运维的局限性，为TiDB在云上提供云原生场景下智能化运维手段，让TiDB在云上自动化运维的同时，也能智能的说话。

# 背景
当前 TiDB 基于 TiDB Operator 部署在 Kubernetes 上，基于云原生 StateFulSet Workload 部署和运行。基于此当前运维和管理有很多局限性，运维不够智能化，没有可观测性的界面了解云上集群状态和运维动作。
我们希望提供一个云上智能化运维解决方案,解决以下问题:
- 时刻保证最佳的运维方式变更。当前TiDB云原生实例更新策略采用Partition倒序更新的方式，没有考虑集群节点当前状态。存在PD节点类型leader迁移两次；TiKV倒序更新节点可能会让集群陷入一个更糟糕的情况，比如TiKV-0因资源问题Crash，应该优先处理TiKV-0节点。
- 解决异构集群的分区运维问题。当前异构集群是通过启动两个不同规格的TiDB负载组合成一个TiDB集群，虽然它们本身是一个集群，但是运维更新没有统一。  
- 让云上TiDB自动化运维的同时能够说话，为用户解决 Operator 自动化运维黑盒问题。当前云原生部署TiDB,没有一个可观测性的视图，查看当前集群状态和云上运维事件变更的信息。

# 项目设计
云上智能化运维的前提是运维更新的策略可以自定义。TiDB采用`Statefulset`部署，我们有两种改造方式:
- 类似于 [ES 云原生项目](https://github.com/elastic/cloud-on-k8s),
- 
