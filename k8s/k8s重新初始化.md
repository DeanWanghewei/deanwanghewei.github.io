# k8s重新初始化
1、所有节点（master和node）重置：kubeadm reset

2、我修改了配置文件（所有master节点），所以重新配置一下： kubeadm config images pull --config ./kubeadm-config.yaml

3、初始化(master1主节点)：kubeadm init --config kubeadm-config.yaml --upload-certs

4、将master2、master3和所有node节点加入集群：参考 https://blog.csdn.net/qq_26900081/article/details/109331192

5、执行以下命令解决错误，需要重新配置这个目录.kube和文件：

错误信息：Unable to connect to the server: x509: certificate signed by unknown authority (possibly because of "crypto/rsa: verification error" while trying to verify candidate authority certificate "kubernetes")

[root@localhost ~]# rm -rf $HOME/.kube
[root@localhost ~]# mkdir -p $HOME/.kube
[root@localhost ~]# sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
[root@localhost ~]# sudo chown $(id -u):$(id -g) $HOME/.kube/config
6、重新安装Calico：参考https://blog.csdn.net/qq_26900081/article/details/109331192第四节

7、按需重新安装Metrics和Dashboard、kuboard：参考https://blog.csdn.net/qq_26900081/article/details/109337475