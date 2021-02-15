# 使用说明

为了方便快速搭建一个单节点的k3s虚拟机，进行开发或测试。

### 使用方法：
1. 安装[VirtualBox](https://www.virtualbox.org/wiki/Downloads)和[Vagrant](https://www.vagrantup.com/downloads)，最新版即可
2. git clone https://github.com/linyang0625/k3s-vagrant.git
3. cd k3s-vagrant
4. 目前支持Centos 7和Ubuntu 20.04 LTS两种虚拟机系统，进入相应的`centos`或者`ubuntu`目录：

        # ~/workspace/my-projects/k3s-vagrant [main o (340e15e)] 
        ▶ ls -l 
        total 16
        -rw-r--r-- 1 linyang 11324 Feb 12 13:13 LICENSE
        -rw-r--r-- 1 linyang  2626 Feb 12 13:13 README.md
        drwxr-xr-x 4 linyang   128 Feb 13 11:52 centos
        drwxr-xr-x 4 linyang   128 Feb 12 13:14 ubuntu
        
5. `vagrant up`，将会创建虚拟机及在虚拟机内安装k3s，初次安装由于需要拉取centos/ubuntu的镜像，视网络情况可能需要20分钟左右
6. 最后看见以下信息时，表示安装已完成：

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


7. 使用命令`vagrant ssh`可以SSH到创建的虚拟机内部对k3s进行操作

       # ~/workspace/my-projects/k3s-vagrant [main * (0e30892)] 
       ▶ vagrant ssh 
       Last login: Sat Jan 16 10:59:55 2021 from 10.0.2.2
       [vagrant@k3s ~]$
       [vagrant@k3s ~]$ kubectl get all
       NAME                 TYPE        CLUSTER-IP   EXTERNAL-IP   PORT(S)   AGE
       service/kubernetes   ClusterIP   10.43.0.1    <none>        443/TCP   151m

8. `vagrant halt`将虚拟机关机，下次`vagrant up`即可再次开机使用

        # ~/workspace/my-projects/k3s-vagrant [main o (b59a74a)] 
        ▶ vagrant halt
        ==> k3s: Attempting graceful shutdown of VM...

        # ~/workspace/my-projects/k3s-vagrant [main o (b59a74a)] 
        ▶ 
        
9. `vagrant destroy`，彻底销毁虚拟机，再次使用时需要重新创建

        # ~/workspace/my-projects/k3s-vagrant 
        ▶ vagrant destroy
            k3s: Are you sure you want to destroy the 'k3s' VM? [y/N] y
        ==> k3s: Forcing shutdown of VM...
        ==> k3s: Destroying VM and associated drives...

        # ~/workspace/my-projects/k3s-vagrant 

默认创建的虚拟机IP为**192.168.77.100**，如果需要更改，请修改Vagrantfile的第三行：
> $k3s_ip = "192.168.77.100"
