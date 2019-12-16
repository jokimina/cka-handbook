# kubernetes 中的 api

## 概述

`Kubernetes API` 是系统描述性配置的基础. `Kubectl` 命令行工具被用于创建、更新、删除、获取API对象.

`Kubernetes` 通过API资源存储自己序列化状态(现在存储在etcd).

`Kubernetes` 被分成多个组件,各部分通过API相互交互

具体规范见: https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api-conventions.md

## api 变更

变更规范见: https://github.com/kubernetes/community/blob/master/contributors/devel/sig-architecture/api_changes.md

## api 定义

Kubernetes使用 `Swagger` 与 `OpenAPI` 记录API所有细节

Swagger 1.2:

- 可以在 `apiserver` 上添加 `-enable-swagger-ui=true` 开启, 暴露端点 `/swaggerapi`, 浏览器访问uri `/swagger-ui`
- `1.14` 版本被移除

Openapi (swagger 2.0):

- `1.10` 版本开始使用 `Openapi`, 通过 `/openapi/v2` 暴露

## api 版本
为了使删除字段或者重构资源表示更加容易,Kubernetes 支持多个API版本.每一个版本都在不同API路径下,例如 /api/v1 或者 /apis/extensions/v1beta1.

主要版本格式如下:

- Alpha 测试版本：

  - 版本名称包含了 alpha (例如：v1alpha1).

  - 可能是有缺陷的.启用该功能可能会带来隐含的问题,默认情况是关闭的.

  - 支持的功能可能在没有通知的情况下随时删除.

  - API的更改可能会带来兼容性问题,但是在后续的软件发布中不会有任何通知.

  - 由于bugs风险的增加和缺乏长期的支持,推荐在短暂的集群测试中使用.

- Beta 测试版本：

  - 版本名称包含了 beta (例如: v2beta3).

  - 代码已经测试过.启用该功能被认为是安全的,功能默认已启用.

  - 所有已支持的功能不会被删除,细节可能会发生变化.

  - 对象的模式和/或语义可能会在后续的beta测试版或稳定版中以不兼容的方式进行更改. 发生这种情况时,我们将提供迁移到下一个版本的说明. 这可能需要删除、编辑和重新创建API对象.执行编辑操作时需要谨慎行事,这可能需要停用依赖该功能的应用程序.

  - 建议仅用于非业务关键型用途,因为后续版本中可能存在不兼容的更改. 如果您有多个可以独立升级的集群,则可以放宽此限制.

  - 请尝试我们的 beta 版本功能并且给出反馈！一旦他们退出 beta 测试版, 我们可能不会做出更多的改变

- 稳定版本：
  - 版本名称是 vX,其中 X 是整数.

  - 功能的稳定版本将出现在许多后续版本的发行软件中.

## api 组

- 核心/遗留组 (core group): 
  - rest路径:`/api/v1`
  - 声明式表示: `apiVersion: v1`
- 命名组 (named group):
  - rest路径: `/apis/$GROUP_NAME/$VERSION`
  - 声明式标识: `apiVersion: $GROUP_NAME/$VERSION`,例如: `apiVersion: batch/v1`
  - 已有可参考: https://kubernetes.io/docs/reference/

- CRD (CustomResourceDefinition): 自定义资源定义, 参考 https://kubernetes.io/docs/tasks/access-kubernetes-api/custom-resources/custom-resource-definitions/
- API Aggregation: 允许在不修改Kubernetes核心代码的同时扩展Kubernetes API, 具体参考: https://kubernetes.io/docs/tasks/access-kubernetes-api/setup-extension-api-server/#setup-an-extension-api-server-to-work-with-the-aggregation-layer

## 启用/禁用 api 组

可以在 `apiserver` 上设置 `--runtime-config` 启用或禁用, 多个资源使用 `,` 分隔

启用:
- api 组: `--runtime-config=batch/v2alpha1`
- api 组中资源: `--runtime-config=extensions/v1beta1/resource`

禁用:
- api 组: `--runtime-config=batch/v2alpha1=false`
- api 组中资源: `--runtime-config=extensions/v1beta1/resouce=false`

## 官方相关页面
- https://kubernetes.io/docs/concepts/overview/kubernetes-api/
