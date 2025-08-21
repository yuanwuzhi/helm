# 运维部署优化
下面是helm 安装组件的命令。可根据需要改进。
## 1.安装nfs 

```shell
helm install nfs-provisioner nfs-subdir-external-provisioner/nfs-subdir-external-provisioner \
  --namespace haios \
  --set nfs.server=192.168.3.161 \
  --set nfs.path=/data/nfs \
  --set storageClass.name=nfs-client \
  --set storageClass.defaultClass=true
```

## 2.安装rustfs(待更新)



## 3.安装redis

```shell
helm install redis bitnami/redis \
  --namespace haios \
  --set architecture=standalone \
  --set auth.password="haios_asimov" \
  --set master.persistence.storageClass=nfs-client \
  --set master.persistence.size=1Gi \
  --set master.resources.requests.cpu="500m" \
  --set master.resources.requests.memory="512Mi" \
  --set master.resources.limits.cpu="1" \
  --set master.resources.limits.memory="1Gi" \
  --set replica.resources.requests.cpu="200m" \
  --set replica.resources.requests.memory="256Mi" \
  --set replica.resources.limits.cpu="500m" \
  --set replica.resources.limits.memory="512Mi"
```



## 4.安装mysql 

```shell
helm install mysql-cluster bitnami/mysql \
  --namespace haios \
  --set auth.rootPassword="asimov" \
  --set auth.database="haios_db" \
  --set auth.username="haios_d2vm" \
  --set auth.password="haios_asimov" \
  --set service.type="NodePort" \
  --set primary.persistence.storageClass="nfs-client" \
  --set primary.resources.requests.cpu="1" \
  --set primary.resources.requests.memory="2Gi" \
  --set primary.resources.limits.cpu="2" \
  --set primary.resources.limits.memory="4Gi" \
  --set secondary.resources.requests.cpu="500m" \
  --set secondary.resources.requests.memory="1Gi" \
  --set secondary.resources.limits.cpu="1" \
  --set secondary.resources.limits.memory="2Gi"
```

