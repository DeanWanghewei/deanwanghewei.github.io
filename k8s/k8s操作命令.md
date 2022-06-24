# k8s 操作命令行
## 查看node 节点
```bash
kubectl get nodes
```
## 安装应用
```bash
# 通过本地文件安装
kubectl apply -f application.yaml

# 通过网路地址安装
kubectl apply -f https://github.com/kubesphere/ks-installer/releases/download/v3.2.1/kubesphere-installer.yaml
```
## 卸载应用
```bash
# 卸载应用。可以指定安装该应用时的配置文件
kubectl delete -f application.yaml
```
## 查看命名空间
```bash
kubectl get ns
```

## k8s删除Terminating状态的命名空间
```bash
查看kubesphere-system的namespace描述

kubectl get ns kubesphere-system  -o json > kubesphere-system.json


编辑json文件，删除spec字段的内存，因为k8s集群时需要认证的。

vi kubesphere-system.json
将

"spec": {
        "finalizers": [
            "kubernetes"
        ]
    },
更改为：

"spec": {
     "finalizers": [
        ]
  },


最后运行curl命令进行删除
kubectl replace --raw "/api/v1/namespaces/kubesphere-system/finalize" -f ./kubesphere-system.json
注意：命令中的kubesphere-system就是命名空间。

```