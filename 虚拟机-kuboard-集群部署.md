## 一、虚拟机配置

| 机器                                        | IP              | 配置              |
| ------------------------------------------- | --------------- | ----------------- |
| 普通机器（安装kuboard-spay、kuboard、其他） | 192.168.223.100 | 2C/2G内存/20G硬盘 |
| k8smaster                                   | 192.168.223.101 | 2C/4G内存/30G硬盘 |
| k8snode1                                    | 192.168.223.102 | 2C/4G内存/30G硬盘 |
| k8snode2                                    | 192.168.223.103 | 2C/4G内存/30G硬盘 |

0.准备：

[下载 VM](https://www.vmware.com/go/getworkstation-win)

[下载 CentOS-7-x86_64-DVD-2009.iso](https://mirrors.aliyun.com/centos/7/isos/x86_64)

1.安装虚拟机

![image](https://user-images.githubusercontent.com/34562805/204071696-16af9cfc-c36f-4d12-8145-9a004d4f5857.png)

创建虚拟机，一路点击下一步，需要注意的几点：

* 选择自定义安装
* 选择稍后安装操作系统
* 网络使用NAT即可

完成后配置ISO映像文件为下载好的centos7：

![image](https://user-images.githubusercontent.com/34562805/204071759-998e6da5-18bb-4b4f-a139-c15d67923fd2.png)

开启虚拟机，直到出现centos安装界面；

![image](https://user-images.githubusercontent.com/34562805/204071878-fb5307b0-dfa8-4f5d-8528-94b207f33702.png)

选择界面语言中文，并配置以上几项，网络和主机名可以不用在这里配置，开始安装，配置root密码，等待完成。

2.配置虚拟机网络

修改网卡配置：

**vim /etc/sysconfig/network-scripts/ifcfg-ens33**

查看自己虚拟网络配置中的子网IP和网关地址：

![image](https://user-images.githubusercontent.com/34562805/204072383-6c63f863-6bcd-4454-82ed-3ef44c8428c3.png)

按照自己虚拟机的ip规划进行静态ip设置，例如：

![image](https://user-images.githubusercontent.com/34562805/204072452-bc30bc7e-1bbb-4f8b-b0db-aedf74e21154.png)

网络重启：**service network restart**

测试是否联通外网：

![image](https://user-images.githubusercontent.com/34562805/204072482-86656b3b-9893-4a74-a9f0-588c0956e24b.png)

3.虚拟机配置

配置k8smaster、k8snode1、k8snode2，参考[这篇](https://juejin.cn/post/6950166816182239246)和[这篇](https://blog.51cto.com/u_5147178/5741190)文章的环境配置。

## 二、安装k8s

1.安装kuboard-spay并安装k8s集群

下载一个资源包：

![image](https://user-images.githubusercontent.com/34562805/204082816-8c1323c8-560d-48ed-9b12-497caf499ebb.png)

创建集群：

![image](https://user-images.githubusercontent.com/34562805/204082906-27b09e21-e925-4b8c-9c3f-887a1d708e3c.png)

连接创建的虚拟机，配置控制节点和工作节点：

![image](https://user-images.githubusercontent.com/34562805/204082971-0eafc206-a369-4853-9e29-b521fe36b943.png)

2.kuboard操作集群

集群安装后，使用kuboard操作集群：

![image](https://user-images.githubusercontent.com/34562805/204083027-37907ede-c30f-425e-b612-6c793c489509.png)

![image](https://user-images.githubusercontent.com/34562805/204083072-f05f9f03-ba1a-4b63-bc10-33d0a4063ed4.png)