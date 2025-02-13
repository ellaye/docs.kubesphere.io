---
title: "前提条件（开发中）"
keywords: 'kubesphere, kubernetes, docker, helm, jenkins, istio, prometheus'
description: ''
---

KubeSphere 支持离线和在线的方式部署至现有的 Kubernetes 集群，部署之前请确保您的 Kubernetes 环境满足以下 4 个前提条件：


- `Kubernetes` 版本 `>=1.13.0`
- `Helm`，版本 `>= 2.10.0`
- 集群可用`内存 >= 10G` 
- 建议配合持久化存储使用（可选）

## 验证环境

1. 确认现有的 `Kubernetes` 版本 `>=1.13.0`，KubeSphere 依赖 `Kubernetes 1.13.0` 版本之后的新特性，可以在执行 `kubectl version` 来确认 :

```bash
$ kubectl version | grep Server
Server Version: version.Info{Major:"1", Minor:"13", GitVersion:"v1.13.5", GitCommit:"2166946f41b36dea2c4626f90a77706f426cdea2", GitTreeState:"clean", BuildDate:"2019-03-25T15:19:22Z", GoVersion:"go1.11.5", Compiler:"gc", Platform:"linux/amd64"}
```

> 说明：注意输出结果中的 `Server Version` 这行，如果显示 `GitVersion` 大于 `v1.13.0`，Kubernetes 的版本是可以安装的。如果低于 `v1.13.0` ，可以查看 [Upgrading kubeadm clusters from v1.12 to v1.13](https://v1-13.docs.kubernetes.io/docs/tasks/administer-cluster/kubeadm/kubeadm-upgrade-1-13/) 先升级下 K8s 版本。

2. 确认已安装 `Helm`，并且 `Helm` 的版本至少为 `2.10.0`。在终端执行 `helm version`，得到类似下面的输出：

```bash
$ helm version
Client: &version.Version{SemVer:"v2.13.1", GitCommit:"618447cbf203d147601b4b9bd7f8c37a5d39fbb4", GitTreeState:"clean"}
Server: &version.Version{SemVer:"v2.13.1", GitCommit:"618447cbf203d147601b4b9bd7f8c37a5d39fbb4", GitTreeState:"clean"}
```

> 说明：
> - 如果提示 `helm: command not found`, 表示还未安装 `Helm`。参考这篇 [Install Helm](https://helm.sh/docs/using_helm/#from-the-binary-releases) 安装 `Helm`, 安装完成后执行  `helm init`；
> - 如果 `helm` 的版本比较老 (<2.10.0), 需要首先升级，参考 [Upgrading Tiller](https://github.com/helm/helm/blob/master/docs/install.md#upgrading-tiller) 升级。

3. 集群现有的可用内存至少在 `10G` 以上。 如果是执行的 `allinone` 安装，那么执行 `free -g` 可以看下可用资源

```bash
root@kubernetes:~# free -g
              total        used        free      shared  buff/cache   available
Mem:              16          4          10           0           3           2
Swap:             0           0           0
```

4. (非必须) KubeSphere 非常建议配合持久化存储使用，执行 `kubectl get sc` 看下当前是否设置了默认的 `storageclass`。

```bash
root@kubernetes:~$ kubectl get sc
NAME                      PROVISIONER               AGE
ceph                      kubernetes.io/rbd         3d4h
csi-qingcloud (default)   disk.csi.qingcloud.com    54d
glusterfs                 kubernetes.io/glusterfs   3d4h
```

> 提示：若未设置持久化存储，安装将默认使用 hostpath，该方式能顺利安装，但可能会由于 Pod 漂移带来其它问题，正式环境建议配置 StorageClass 使用持久化存储。

如果你的 Kubernetes 环境满足以上的要求，那么可以接着执行下面的步骤了。