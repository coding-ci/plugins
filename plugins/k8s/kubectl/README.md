# kubectl

Kubectl 是 Kubernetes 命令行接口。通过 Kubectl 命令可以方便的管理 Kubernetes 集群。

Kubectl 同样可以管理腾讯云 tke 集群。

## 在 Coding-CI 上使用

```yml
master:
  push:
    - stages:
      - name: 使用 kubectl 操作腾讯 TKE 更新指定pod的镜像版本
      # 可参考导入帮助手册环境变量相关
        imports: https://xxx/kube-config
        image: bitnami/kubectl
        commands: |
          echo -n $KUBECF > ~/.kube/config
          kubectl set image $POD_TYPE/$POD $CONTAINER=$IMAGE:$TAG -n $NS
 ```

## 参数含义

- `$POD` - pod 的名字
- `$POD_TYPE` - pod 类型，常见如 `Deployment\StatefulSet` 等
- `$CONTAINER` - pod 中容器的名字
- `$IMAGE` - 期望部署的 docker 镜像名
- `$IMAGE_TAG` - 是镜像标签

## kube-config

```json
KUBECF={"apiVersion":"v1","clusters":[{"cluster":{"certificate-authority-data":"xxx","server":"https://123.20.11.21:443/"},"name":"cls-1m6x0bbo"}],"contexts":[{"context":{"cluster":"cls-1m6x0bbo","user":"100014140xxx"},"name":"cls-1m6x0bbo-100014140xxx-context-default"}],"current-context":"cls-1m6x0bbo-100014140xxx-context-default","kind":"Config","preferences":{},"users":[{"name":"100014140xxx","user":{"client-certificate-data":"xxx","client-key-data":"xxx"}}]}
```

`kube-config` 的具体内容，可以从腾讯云控制台，集群「基本信息」中的「集群 APIServer 信息」中获取。

## 更多用法

更多用法参考：

- [kubernetes/kubectl](https://github.com/kubernetes/kubectl)
- [kubectl文档](https://kubernetes.io/docs/reference/generated/kubectl/kubectl-commands)
- [bitnami/kubectl文档](https://github.com/bitnami/containers/tree/main/bitnami/kubectl)
- [entrypoint](https://yeasy.gitbook.io/docker_practice/image/dockerfile/entrypoint)
- [导入环境变量](https://ci.coding.net/docs/env.html#dao-ru-huan-jing-bian-liang)
