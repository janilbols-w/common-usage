# Docker Swarm容器集群管理工具
source: https://jiayi.space/post/docker-swarmrong-qi-ji-qun-guan-li-gong-ju
author: Melw00d
date: 2018 March 01
```
!!! this tutorial is a copy, should there be any legal issue please contact me directly.
This page is only used for technique sharing.
```

Docker Swarm 是在 Docker 1.12版本之后添加的容器集群管理工具，可以统一管理分布在不同主机的多个容器。相比起Kubenetes，Docker Swarm无需额外安装，只要有较新版本的Docker就可以使用。如果你尝试过搭建Kubenetes，就知道这差别有多大。之前趁着参加Dell EMC的比赛学习实践了一把Docker Swarm，感觉真不愧是Docker的自带工具，一如既往的简单好用。在这里总结下它用到的一些技术原理和使用方法。

## 设计架构
![Architecture](https://jiayi.space/_image/swarmarchitecture.jpg)

因为是集成在Docker之中，由Docker Client向Swarm发送指令。每个Docker engine实例称为一个Node，既可以是物理机，也可以是虚拟机。分为manager和worker。worker只负责接收并执行任务，manager在此基础上还要接收用户指令，服务调度，服务发现...

![](https://jiayi.space/_image/services-diagram.png)
另一个重要的概念是service，通常服务是一个大的应用分割出来的小的功能单元（microservice）。比如一个web应用中，nginx是一个service，mysql是一个service，php是一个service。
而task，就是指容器中执行的具体命令。


# Please go to the original [page](https://jiayi.space/post/docker-swarmrong-qi-ji-qun-guan-li-gong-ju) for further infomation
