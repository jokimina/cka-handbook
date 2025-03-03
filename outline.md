# 考试大纲

基于 `curriculum 1.14.1`

官方会不定期在 https://github.com/cncf/curriculum 进行更新

* 19% - 核心概念
  * [kubernetes api](core-concept/kubernetes-api-primitive.md)
    * [kubernetes object](core-concept/kubernetes-object.md)
  * [kubernetes 集群架构](core-concept/kubernetes-architecture/index.md)
  * `Services` 和其他网络组件
* 5% - 调度
  * 使用 `label selector` 调度poPd
  * `DeamonSets` 的角色
  * `resources limit` 如何影响pod调度
  * 如何运行多个调度器并且知道如何配置 `Pod` 使用他们
  * 查看调度事件
  * 如何配置 `kubernetes` 的调度器
* 5% - 日志/监控
  * 如何监控集群所有组件
  * 如何监控应用
  * 管理集群组件日志
  * 管理应用日志
* 8% - 应用生命周期管理
  * `Deployments` 和如何处理滚动更新以及回滚
  * 使用各种方式配置应用
  * 如何调整应用规模
  * 如何通过必要组件创建自愈应用
* 11% - 集群
  * 如何处理集群升级
  * 如何升级操作系统
  * 备份和恢复的方法
* 12% - 安全
  * 如何配置认证和授权
  * 集群的安全组件
  * 如何配置网络策略
  * 如何为集群组件创建和管理集群 `TLS` 证书
  * 使用安全的镜像
  * 定义安全上下文
  * 安全持久化的键值存储
* 7% - 存储
  * 如何持久化数据卷和知道如何创建它们
  * 数据卷的访问模式
  * 存储卷声明组件
  * `kubernetes` 存储对象
  * 如何配置使用持久化数据卷的应用
* 10% - 故障排查
  * 排查应用故障
  * 排查控制面板故障
  * 排查工作节点故障
  * 排查网络
* 11% - 网络
  * 集群节点的网络配置
  * `Pod` 网络概念
  * `Services` 网络
  * 部署和配置网络负载均衡
  * 如何使用 `Ingress` 规则
  * 如何配置和使用集群 `DNS`
  * 什么是 `CNI`
* 12% - 安装, 配置, 验证
  * 设计一个 `Kubernetes` 集群
  * 安装 `Kubernetes` 的主节点和工作节点
  * 配置集群的安全通信
  * 配置一个高可用集群
  * 获取 `Kubernetes` 的二进制发行版
  * 提供基础设施部署 `Kubernetes` 集群
  * 选择一个网络解决方案
  * 选择你的 `Kubernetes` 基础配置
  * 在你的集群上运行 `e2e` (端到端)测试
  * 分析e2e测试结果
  * 运行节点的e2e测试
  * 安装和使用 `kubeadmin` 来安装, 配置, 管理 `Kubernetes` 集群
  