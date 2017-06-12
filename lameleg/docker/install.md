yum install -y yum-utils
yum-config-manager     --add-repo     https://download.docker.com/linux/centos/docker-ce.repo
yum-config-manager --disable docker-ce-edge
yum makecache fast
yum install docker-ce
service docker start

卸载docker :
1.13以上：
yum remove docker-ce

以下：
yum remove docker\docker-common\container-selinux\docker-selinux\docker-engine

