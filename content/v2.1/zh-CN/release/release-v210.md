---
title: "Release Notes For 2.1.0（Dev 版）"
keywords: 'kubernetes, docker, helm, jenkins, istio, prometheus'
description: 'KubeSphere Release Notes'
---

KubeSphere 2.1.0 目前公开的 Installer 是 dev 版，方便社区用户在 2.1.0 GA 发布前的公测与体验，因此当前版本不建议用于正式环境。若在安装使用中遇到问题或发行 Bug，欢迎提交到 [GitHub issue](https://github.com/kubesphere/kubesphere/issues/new/choose)，产品使用问题与技术交流请在 [开发者社区](https://kubesphere.io/forum/) 提问。

## Installer 改进

### Features


- 核心组件解耦，可选装 DevOps、微服务治理（Service Mesh）、应用商店、日志、告警通知等模块

- 增加 Grafana 可选安装组件，默认版本 5.2.4

- Kubernetes 支持升级至 1.15.5，兼容 1.4.x 和 1.3.x

- [OpenPitrix](https://openpitrix.io) 应用商店后端管理模块升级至 0.4

- 升级日志采集组件 Fluent Bit 至 v1.2.1

- 升级 DevOps 组件 Jenkins 至 v2.176.2

- Istio 组件升级至 1.3.2 



## 应用商店

### Features


- 支持应用上传、审批、分类，提供内置应用仓库和应用



### UPGRADE & ENHANCEMENT


- 应用仓库(模板) 由Global 级别调整至 企业空间(WorkSpace)

- 支持企业空间管理员设置应用仓库



## 存储

### Features


- 支持 Dynamic Local Volume

- 为 QingCloud 云平台块存储提供实时监控功能



### UPGRADE & ENHANCEMENT


- QingCloud CSI 插件适配 CSI 1.1.0，支持扩容、拓扑、创建/删除快照以及基于快照创建 pvc



### BUG FIXES


- 修复存储类型列表存储卷的显示错误



## 可观察性

### Features


- 对于将日志以文件形式保存在 Pod 挂盘上的应用，新增在 UI 上开启落盘日志收集功能

- 支持对接 ElasticSearch 7.x

- 支持中文日志检索

- 支持 initContainer 日志的展示

- 支持日志导出

- 新增告警解除通知



### UPGRADE & ENHANCEMENT


- 优化日志检索速度

- 优化日志服务异常时的提示信息

- 优化监控数据请求异常时的返回信息

- 增加 Prometheus Pod 反亲和性



### BUG FIXES


- 修复日志搜索高亮文字不正确的问题

- 修复日志搜索不能正确匹配短语

- 修复按工作负载名搜索日志时，无法查询到已删除工作负载的日志

- 修复日志高亮时，显示结果被截断

- 修复部分指标异常：节点 inode 、最大 pod 容纳量指标

- 修复告警目标数量错误的问题

- 修复多指标监控的过滤失效问题

- 修复自定义污点节点无日志、监控信息的问题（调整了 node-exporter、fluent-bit 的 Toleration 属性，默认将部署在所有节点上，忽略节点污点）


## DevOps

### Features


- s2i 支持切换分支和git日志的输出

- b2i（Binary To Image），支持将 Linux Binary/war/jar 三种交付物一键构建镜像

- 为流水线、s2i、b2i 提供代码依赖缓存支持

- 流水线部署步骤支持删除 Kubernetes 资源

- 多分支流水线支持在分支创建/删除时触发其他流水线运行



### UPGRADE & ENHANCEMENT


- 流水线增加支持 bitbucket

- 支持流水线 cron 脚本验证

- 支持 Jenkinsfile 语法校验

- 支持 SonarQube 自定义链接

- 支持流水线事件触发构建

- 优化流水线 Agent 节点选择

- 减少流水线启动速度

- 使用动态卷作为流水线 Agent 的工作目录

- 优化 Jenkins kubernetesDeploy 插件，新增更多资源和版本（v1、apps/v1、extensions/v1beta1、apps/v1beta2、apps/v1beta1、autoscaling/v1、autoscaling/v2beta1、autoscaling/v2beta2、networking.k8s.io/v1、batch/v1beta1、batch/v2alpha1）

- 流水线部署步骤新增 PV、PVC、Network Policy 支持



## 认证和权限

### Features


- 支持AD账户同步、认证



### UPGRADE & ENHANCEMENT


- 降低 ldap 组件的内存使用量



### BUG FIXES


- 修复 ldap 连接池泄漏的问题

- 修复企业空间无法添加用户的问题



## 用户体验

### Features


- 向导式纳管未分配到企业空间中的项目（namespace）



### UPGRADE & ENHANCEMENT


- 主机信息展示优化

- 新增邮件服务器测试功能

- 资源列表页新增帮助提示

- 优化项目概览页和项目基本信息

- 优化服务创建流程

- 优化工作负载创建流程

- 优化资源列表状态更新

- 优化 yaml 编辑功能

- 支持镜像检索和镜像信息展示

- 工作负载页面增加 pod 列表

- 更新网页终端页面主题

- 增加容器切换功能

- 优化 pod 信息展示并新增 pod 调度信息



### BUG FIXES


- 修复项目默认请求资源显示错误的问题

- 修复网页终端路径过深的问题

- 修复 Pod 状态更新不及时的问题

- 修复无法基于角色搜索主机的问题