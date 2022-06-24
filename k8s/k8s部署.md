## 安装docker
CentOS
> 警告：切勿在没有配置 Docker YUM 源的情况下直接使用 yum 命令安装 Docker.

### 准备工作
#### 系统要求
Docker 支持 64 位版本 CentOS 7/8，并且要求内核版本不低于 3.10。 CentOS 7 满足最低内核的要求，但由于内核版本比较低，部分功能（如 overlay2 存储层驱动）无法使用，并且部分功能可能不太稳定。
##### 卸载旧版本
旧版本的 Docker 称为 docker 或者 docker-engine，使用以下命令卸载旧版本：

```bash
sudo yum remove docker \
                  docker-client \
                  docker-client-latest \
                  docker-common \
                  docker-latest \
                  docker-latest-logrotate \
                  docker-logrotate \
                  docker-selinux \
                  docker-engine-selinux \
                  docker-engine

```

使用 yum 安装
执行以下命令安装依赖包：

```bash
sudo yum install -y yum-utils
```

鉴于国内网络问题，强烈建议使用国内源，官方源请在注释中查看。
执行下面的命令添加 yum 软件源：
```bash
sudo yum-config-manager \
    --add-repo \
    https://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
​
```
```bash
 sudo sed -i 's/download.docker.com/mirrors.aliyun.com\/docker-ce/g' /etc/yum.repos.d/docker-ce.repo
​
# 官方源
# $ sudo yum-config-manager \
#     --add-repo \
#     https://download.docker.com/linux/centos/docker-ce.repo
```

如果需要测试版本的 Docker 请执行以下命令：
```bash
sudo yum-config-manager --enable docker-ce-test
```
安装 Docker
更新 yum 软件源缓存，并安装 docker-ce。
```bash
sudo yum install docker-ce docker-ce-cli containerd.io
```
CentOS8 额外设置
由于 CentOS8 防火墙使用了 nftables，但 Docker 尚未支持 nftables， 我们可以使用如下设置使用 iptables：
更改 /etc/firewalld/firewalld.conf
```bash
# FirewallBackend=nftables
FirewallBackend=iptables
```
或者执行如下命令：
```bash
firewall-cmd --permanent --zone=trusted --add-interface=docker0
firewall-cmd --reload
```

使用脚本自动安装
在测试或开发环境中 Docker 官方为了简化安装流程，提供了一套便捷的安装脚本，CentOS 系统上可以使用这套脚本安装，另外可以通过 --mirror 选项使用国内源进行安装：
若你想安装测试版的 Docker, 请从 test.docker.com 获取脚本
```bash
# $ curl -fsSL test.docker.com -o get-docker.sh
curl -fsSL get.docker.com -o get-docker.sh
sudo sh get-docker.sh --mirror Aliyun
```
# $ sudo sh get-docker.sh --mirror AzureChinaCloud
执行这个命令后，脚本就会自动的将一切准备工作做好，并且把 Docker 的稳定(stable)版本安装在系统中。
启动 Docker
$ sudo systemctl enable docker
$ sudo systemctl start docker
建立 docker 用户组
默认情况下，docker 命令会使用  与 Docker 引擎通讯。而只有 root 用户和 docker 组的用户才可以访问 Docker 引擎的 Unix socket。出于安全考虑，一般 Linux 系统上不会直接使用 root 用户。因此，更好地做法是将需要使用 docker 的用户加入 docker 用户组。
建立 docker 组：
$ sudo groupadd docker
将当前用户加入 docker 组：
$ sudo usermod -aG docker $USER
退出当前终端并重新登录，进行如下测试。
测试 Docker 是否安装正确
$ docker run --rm hello-world
​
Unable to find image 'hello-world:latest' locally
latest: Pulling from library/hello-world
b8dfde127a29: Pull complete
Digest: sha256:308866a43596e83578c7dfa15e27a73011bdd402185a84c5cd7f32a88b501a24
Status: Downloaded newer image for hello-world:latest
​
Hello from Docker!
This message shows that your installation appears to be working correctly.
​
To generate this message, Docker took the following steps:
 1. The Docker client contacted the Docker daemon.
 2. The Docker daemon pulled the "hello-world" image from the Docker Hub.
    (amd64)
 3. The Docker daemon created a new container from that image which runs the
    executable that produces the output you are currently reading.
 4. The Docker daemon streamed that output to the Docker client, which sent it
    to your terminal.
​
To try something more ambitious, you can run an Ubuntu container with:
 $ docker run -it ubuntu bash
​
Share images, automate workflows, and more with a free Docker ID:
 https://hub.docker.com/
​
For more examples and ideas, visit:
 https://docs.docker.com/get-started/
若能正常输出以上信息，则说明安装成功。
镜像加速
如果在使用过程中发现拉取 Docker 镜像十分缓慢，可以配置 Docker 。
添加内核参数
如果在 CentOS 使用 Docker 看到下面的这些警告信息：
WARNING: bridge-nf-call-iptables is disabled
WARNING: bridge-nf-call-ip6tables is disabled
请添加内核配置参数以启用这些功能。
$ sudo tee -a /etc/sysctl.conf <<-EOF
net.bridge.bridge-nf-call-ip6tables = 1
net.bridge.bridge-nf-call-iptables = 1
EOF
然后重新加载 sysctl.conf 即可
$ sudo sysctl -p


## 错误问题解决
### 安装 kubectl
```bash
[root@hadoop-slave02 etc]# yum install -y kubelet kubeadm kubectl
已加载插件：fastestmirror
Loading mirror speeds from cached hostfile
 * base: mirrors.aliyun.com
 * extras: mirrors.aliyun.com
 * updates: mirrors.aliyun.com
kubernetes/signature                                                                                                                                           |  844 B  00:00:00
从 https://mirrors.aliyun.com/kubernetes/yum/doc/yum-key.gpg 检索密钥
从 https://mirrors.aliyun.com/kubernetes/yum/doc/rpm-package-key.gpg 检索密钥
kubernetes/signature                                                                                                                                           | 1.4 kB  00:00:01 !!!
https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/repodata/repomd.xml: [Errno -1] repomd.xml signature could not be verified for kubernetes
正在尝试其它镜像。


 One of the configured repositories failed (Kubernetes),
 and yum doesn't have enough cached data to continue. At this point the only
 safe thing yum can do is fail. There are a few ways to work "fix" this:

     1. Contact the upstream for the repository and get them to fix the problem.

     2. Reconfigure the baseurl/etc. for the repository, to point to a working
        upstream. This is most often useful if you are using a newer
        distribution release than is supported by the repository (and the
        packages for the previous distribution release still work).

     3. Run the command with the repository temporarily disabled
            yum --disablerepo=kubernetes ...

     4. Disable the repository permanently, so yum won't use it by default. Yum
        will then just ignore the repository until you permanently enable it
        again or use --enablerepo for temporary usage:

            yum-config-manager --disable kubernetes
        or
            subscription-manager repos --disable=kubernetes

     5. Configure the failing repository to be skipped, if it is unavailable.
        Note that yum will try to contact the repo. when it runs most commands,
        so will have to try and fail each time (and thus. yum will be be much
        slower). If it is a very temporary problem though, this is often a nice
        compromise:

            yum-config-manager --save --setopt=kubernetes.skip_if_unavailable=true

failure: repodata/repomd.xml from kubernetes: [Errno 256] No more mirrors to try.
https://mirrors.aliyun.com/kubernetes/yum/repos/kubernetes-el7-x86_64/repodata/repomd.xml: [Errno -1] repomd.xml signature could not be verified for kubernetes

```
解决方案：
```bash
# 修改repo 文件的信息
repo_gpgcheck=0
```
相关解决连接
https://github.com/kubernetes/kubernetes/issues/60134


## node 节点加入master 报错
```bash
[preflight] Running pre-flight checks
error execution phase preflight: [preflight] Some fatal errors occurred:
        [ERROR CRI]: container runtime is not running: output: time="2022-06-22T16:20:19+08:00" level=fatal msg="unable to determine runtime API version: rpc error: code = Unavailable desc = connection error: desc = \"transport: Error while dialing dial unix /var/run/containerd/containerd.sock: connect: no such file or directory\""
, error: exit status 1
[preflight] If you know what you are doing, you can make a check non-fatal with `--ignore-preflight-errors=...`
To see the stack trace of this error execute with --v=5 or higher
```
