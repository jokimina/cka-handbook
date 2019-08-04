# 理解 kubernetes 对象

## kubernetes 对象

kubernetes 对象是持久化的实体, 用以表示集群的状态.

- 哪些容器在运行(在哪些节点)
- 可以被应用使用的资源
- 应用运行时表现策略, 重启策略, 升级策略, 容错策略等

Kubernetes 对象是 "目标性记录", 一旦创建对象,Kubernetes 系统将持续工作以确保对象存在.通过创建对象,本质上是在告知 Kubernetes 系统,所需要的集群工作负载看起来是什么样子的,这就是 Kubernetes 集群的 期望状态(Desired State). 即 **声明式**

操作 Kubernetes 对象, 无论是创建, 修改, 或者删除, 需要使用 Kubernetes API.比如,当使用 kubectl 命令行接口时,CLI 会执行必要的 Kubernetes API 调用,也可以在程序中直接调用 Kubernetes API.

各种语言SDK地址: https://kubernetes.io/docs/reference/using-api/client-libraries/

## 对象规约(Spec)与状态(Status)

每个 Kubernetes 对象包含两个嵌套的对象字段它们负责
- Spec: 描述了期望的状态 (Desired State)
- Status: 描述了实际的状态 (Actual State)

## 描述 Kubernetes 对象

创建 kubernetes 对象时, 必须提供 `Spec` 描述期望的状态以及对象的一些基本信息(比如名称等)

使用 Kubernetes API 创建对象时(或者直接创建, 或者基于kubectl)API 请求必须在请求体中包含 JSON 格式的信息. 大多数情况下, 需要在 .yaml 文件中为 kubectl 提供这些信息. kubectl 在发起 API 请求时,将这些信息转换成 JSON 格式.

示例:
```yaml
apiVersion: apps/v1 # 1.9.0 版本前使用 apps/v1beta2
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  selector:
    matchLabels:
      app: nginx
  replicas: 2
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.7.9
        ports:
        - containerPort: 80
```

## 必须字段

- apiVersion: 创建该对象所使用的 Kubernetes API 的版本
- kind: 想要创建的对象的类型
- metadata: 帮助识别对象唯一性的数据,包括一个 name 字符串UID, 和可选的 namespace
- spec: 期望状态

## 参考
- https://kubernetes.io/docs/concepts/overview/working-with-objects/kubernetes-objects/
