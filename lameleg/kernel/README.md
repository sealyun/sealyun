## 内核升级
centos7.3默认内核3.10, 为了更好支持高版本docker和overlay存储驱动，将内核升级到4.10以上

更新前，内核版本为：

uname -r  
3.10.0-327.10.1.el7.x86_64
升级的方法：

1、导入key
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org  

2、安装elrepo的yum源
rpm -Uvh http://www.elrepo.org/elrepo-release-7.0-2.el7.elrepo.noarch.rpm  

3、安装内核
yum --enablerepo=elrepo-kernel install  kernel-ml-devel kernel-ml  
当前为4.4.4:
==================================================================================
Package             架构               版本                   源              大小
==================================================================================
正在安装:
 kernel-ml         x86_64      4.4.4-1.el7.elrepo       elrepo-kernel       38 M
 kernel-ml-devel   x86_64      4.4.4-1.el7.elrepo       elrepo-kernel       10 M

4、查看默认启动顺序
awk -F\' '$1=="menuentry " {print $2}' /etc/grub2.cfg  
CentOS Linux (4.4.4-1.el7.elrepo.x86_64) 7 (Core)  
CentOS Linux (3.10.0-327.10.1.el7.x86_64) 7 (Core)  
CentOS Linux (0-rescue-c52097a1078c403da03b8eddeac5080b) 7 (Core)
默认启动的顺序是从0开始，新内核是从头插入（目前位置在0，而4.4.4的是在1），所以需要选择0。

grub2-set-default 0  
然后reboot重启，使用新的内核，下面是重启后使用的内核版本:

uname -r  
4.4.4-1.el7.elrepo.x86_64  

5、删除旧的内核
yum remove kernel  
