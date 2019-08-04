# Master


Master 组件提供对集群的控制, 对集群做出全局性决策(例如：调度),以及检测和响应集群事件

实际使用上 `Master` 会涉及一些高可用的考虑:
- https://kubernetes.io/docs/setup/production-environment/tools/kubeadm/high-availability/
- https://kubernetes.io/docs/tasks/administer-cluster/highly-available-master/

## 组件

- kube-apiserve: 对外暴露了Kubernetes API, 资源操作的唯一入口,并提供认证、授权、访问控制、API注册和发现等机制；
- etcd: 保存了整个集群的状态. 分布式、一致性的键值存储系统,主要用于配置共享和服务发现.
- kube-scheduler: 负责资源的调度,按照预定的调度策略将Pod调度到相应的机器上.
- kube-controller-manager: 运行控制器, 它们是处理集群中常规任务的后台线程. 逻辑上, 每个控制器是一个单独的进程, 但为了降低复杂性, 它们都被编译到一个执行文件,在单个进程中运行
  - 节点控制器 (Node Controller): 当节点移除时,负责通知和响应.
  - 副本控制器 (Replication Controller): 负责维护系统中每个副本控制器对象的 pod 数量.
  - 端点控制器 (Replication Controller): 填充 端点(Endpoints) 对象(连接到 Services & Pods).
  - 服务帐户和令牌控制器 (Service Account & Token Controllers): 为新的命名空间创建默认帐户和 API 访问令牌


- cloud-controller-manager (云环境云厂商会提供):  是用于与底层云提供商交互的控制器, 1.6 版本 `alpha` 形式加入. [更多细节](https://kubernetes.io/docs/concepts/architecture/cloud-controller/)
  - 节点控制器 (Node Controller): 用于检查云提供商以确定节点是否在云中停止响应后被删除
  - 路由控制器 (Route Controller): 用于在底层云基础架构中设置路由
  - 服务控制器 (Service Controller): 用于创建,更新和删除云提供商负载平衡器
  - 数据卷控制器 (Volume Controller): 用于创建,附加和装载卷,并与云提供商进行交互以协调卷

## 参考

- https://kubernetes.io/docs/concepts/overview/components/#master-components
