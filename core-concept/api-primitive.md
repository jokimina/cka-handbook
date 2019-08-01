# kubernetes 中的 api 基本体

## 概述

`Kubernetes API` 是系统描述性配置的基础. `Kubectl` 命令行工具被用于创建、更新、删除、获取API对象。

`Kubernetes` 通过API资源存储自己序列化状态(现在存储在etcd)。

`Kubernetes` 被分成多个组件，各部分通过API相互交互

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

## 官方相关页面
- https://kubernetes.io/docs/concepts/overview/kubernetes-api/