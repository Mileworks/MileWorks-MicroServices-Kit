# MileWorks-MicroServices-Kit
## minikube本地安装实际过程（国内），可按步骤操作即可。  -- 这里基于ubuntu 18.04  
这里教程只是用于实际本地开发 ， 如果要使用k8s用于生产环境，必须搭建高可用HA 的K8s，是到坎，后面章节会说明。这里只针对实际本地开发时候搭建k8s，官方推荐的是minikube。  
### 运行环境  
  ubuntu 18.04 至少这个版本 低了不行 没有snap
  可以访问互联网    
  docker 环境
### 安装步骤  
  更新系统apt包相关资源，需要手动调整到国内的镜像源 不然要慢死人了。  
  安装snap snapd 方便后续安装kubectl：  
  ```
  sudo apt update && sudo apt upgrade   
  sudo apt install snap  snapd  
  ```  
  1：安装kubectl  
  比较懒 采用 snap(类似apt的东西) 安装kubectl
  ```
  sudo snap install kubectl (妈的 这步安装之后始终会报下面的错，后可以从github下载对应版本的kubectl)
  ```
  2：安装golang  
  使用apt 安装golang  
  ```  
  sudo apt install golang
  ```  
  3: 安装minikube  
  ```
  curl -Lo minikube http://kubernetes.oss-cn-hangzhou.aliyuncs.com/minikube/releases/v0.25.0/minikube-linux-amd64 && chmod +x minikube && sudo mv minikube /usr/local/bin/
  ```
  4:启动minikube  
  ```
  minikube start --registry-mirror=https://registry.docker-cn.com
  minikube ssh   
  ```  
  手动拉取镜像： 配合本地docker环境
  阿里的镜像查询地址：https://dev.aliyun.com/search.html
  ```
  docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/kube-addon-manager-amd64:v6.4-beta.2
docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/kube-addon-manager-amd64:v6.4-beta.2 gcr.io/google-containers/kube-addon-manager:v6.4-beta.2

docker pull registry.cn-hangzhou.aliyuncs.com/google-containers/kubernetes-dashboard-amd64:v1.7.0
docker tag registry.cn-hangzhou.aliyuncs.com/google-containers/kubernetes-dashboard-amd64:v1.7.0 gcr.io/google-containers/kubernetes-dashboard-amd64:v1.7.0


docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/k8s-dns-kube-dns-amd64:1.14.5
docker tag registry.cn-hangzhou.aliyuncs.com/google_containers/k8s-dns-kube-dns-amd64:1.14.5 gcr.io/google-containers/k8s-dns-kube-dns-amd64:1.14.5

docker pull registry.cn-hangzhou.aliyuncs.com/google-containers/k8s-dns-dnsmasq-nanny-amd64:1.14.5
docker tag registry.cn-hangzhou.aliyuncs.com/google-containers/k8s-dns-dnsmasq-nanny-amd64:1.14.5 gcr.io/google-containers/k8s-dns-dnsmasq-nanny-amd64:1.14.5

docker pull registry.cn-hangzhou.aliyuncs.com/google-containers/k8s-dns-sidecar-amd64:1.14.5
docker tag registry.cn-hangzhou.aliyuncs.com/google-containers/k8s-dns-sidecar-amd64:1.14.5 gcr.io/google-containers/k8s-dns-sidecar-amd64:1.14.5

docker pull registry.cn-hangzhou.aliyuncs.com/google_containers/kubedns-amd64:1.9
docker tag registry.cn-hangzhou.aliyuncs.com/google-containers/kubedns-amd64:1.9 gcr.io/google-containers/kubedns-amd64:1.9

docker pull registry.cn-hangzhou.aliyuncs.com/google-containers/kube-dnsmasq-amd64:1.4
docker tag registry.cn-hangzhou.aliyuncs.com/google-containers/kube-dnsmasq-amd64:1.4 gcr.io/google-containers/kube-dnsmasq-amd64:1.4

docker pull registry.cn-hangzhou.aliyuncs.com/google-containers/exechealthz-amd64:1.2
docker tag registry.cn-hangzhou.aliyuncs.com/google-containers/exechealthz-amd64:1.2 gcr.io/google-containers/exechealthz-amd64:1.2

docker pull registry.cn-hangzhou.aliyuncs.com/google-containers/echoserver:1.4
docker tag  registry.cn-hangzhou.aliyuncs.com/google-containers/echoserver:1.4 gcr.io/google-containers/echoserver:1.4

docker pull registry.cn-hangzhou.aliyuncs.com/google-containers/pause-amd64:3.0
docker tag registry.cn-hangzhou.aliyuncs.com/google-containers/pause-amd64:3.0 gcr.io/google-containers/pause-amd64:3.0
```

  
  5:尝试kubectl是否可用
```
kubectl get all
```  
注意：  
如果出现如下信息的解决办法：  
```
Error from server (NotAcceptable): unknown (get pods)
```  
先到https://github.com/kubernetes/kubernetes/blob/master/CHANGELOG.md#client-binaries-1 从github上找到对应的client binaries。然后复制连接地址。然后执行以下命令

```
wget https://dl.k8s.io/v1.9.3/kubernetes-client-linux-amd64.tar.gz
tar -zxvf kubernetes-client-linux-amd64.tar.gz
cd kubernetes/client/bin
chmod +x ./kubectl
sudo mv ./kubectl /usr/local/bin/kubectl
```

6:打开k8s web ui  
```
minikube dashboard
```
如果报以下错误信息，解决办法
```
Waiting, endpoint for service is not ready yet...
```

执行完毕后会自动弹出浏览器 如果没有 请尝试 http://192.168.99.100:30000  













  




  

