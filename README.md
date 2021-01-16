# 使用说明

为了方便快速搭建一个单节点的k3s虚拟机，进行开发或测试。

### 使用方法：
1. 安装[VirtualBox](https://www.virtualbox.org/wiki/Downloads)和[Vagrant](https://www.vagrantup.com/downloads)，最新版即可
2. git clone https://github.com/polaristech-io/k3s-vagrant.git
3. cd k3s-vagrant
4. vagrant up，将会创建虚拟机及在虚拟机内安装k3s，初次安装由于需要拉取centos的镜像，视网络情况可能需要20分钟左右
5. 最后看见以下信息时，表示安装已完成：

        k3s: Complete!
        k3s: [INFO]  Creating /usr/local/bin/kubectl symlink to k3s
        k3s: [INFO]  Creating /usr/local/bin/crictl symlink to k3s
        k3s: [INFO]  Creating /usr/local/bin/ctr symlink to k3s
        k3s: [INFO]  Creating killall script /usr/local/bin/k3s-killall.sh
        k3s: [INFO]  Creating uninstall script /usr/local/bin/k3s-uninstall.sh
        k3s: [INFO]  env: Creating environment file /etc/systemd/system/k3s.service.env
        k3s: [INFO]  systemd: Creating service file /etc/systemd/system/k3s.service
        k3s: [INFO]  systemd: Enabling k3s unit
        k3s: Created symlink from /etc/systemd/system/multi-user.target.wants/k3s.service to /etc/systemd/system/k3s.service.
        k3s: [INFO]  systemd: Starting k3s


6. 使用命令vagrant ssh，可以SSH到创建的虚拟机内部对k3s进行操作

       # ~/workspace/my-projects/k3s-vagrant [main * (0e30892)] 
       ▶ vagrant ssh 
       Last login: Sat Jan 16 10:59:55 2021 from 10.0.2.2
       [vagrant@k3s ~]$
       [vagrant@k3s ~]$ kubectl get all
       NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
       service/kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   151m

7. vagrant halt, 将虚拟机关机
8. vagrant destroy, 销毁虚拟机

默认创建的虚拟机IP为**192.168.77.100**，如果需要更改，请修改Vagrantfile的第三行：
> $k3s_ip = "192.168.77.100"
