Centos7 安装配置
postgresql数据库

sudo yum install -y https://download.postgresql.org/pub/repos/yum/reporpms/EL-7-x86_64/pgdg-redhat-repo-latest.noarch.rpm
sudo yum install -y postgresql14-server
sudo /usr/pgsql-14/bin/postgresql-14-setup initdb
sudo systemctl enable postgresql-14
sudo systemctl start postgresql-14
firewall-cmd --zone=public --add-port=端口号/tcp --permanent #开启指定端口
systemctl restart firewalld.service #开启指定端口后必须重启防火墙，重启命令
systemctl status firewalld.service #查看防火墙状态
systemctl start firewalld.service #开启防火墙
systemctl disable firewalld.service #禁止开机启动
systemctl enable firewalld.service #开启开机启动
firewall-cmd --list-ports #查看已开放端口
firewall-cmd --query-port=123/tcp #查询指定端口是否开启成功
firewall-cmd --add-port=123/tcp --permanent #添加指定需要开放的端口
firewall-cmd --permanent --remove-port=123/tcp #移除指定端口

centos 关闭 selinux
1、查看 selinux 状态
>> sestatus

SELinux status:                 enabled`
SELinuxfs mount:                /sys/fs/selinux
SELinux root directory:         /etc/selinux
Loaded policy name:             targeted
Current mode:                   enforcing
Mode from config file:          enforcing
Policy MLS status:              enabled
Policy deny_unknown status:     allowed
Max kernel policy version:      31
2、禁用 SELinux
暂时禁用 SELinux，请在终端中输入以下命令：
 >> sudo setenforce 0
永久禁用 SELinux
 >> vi /etc/sysconfig/selinux
 将 SELINUX=enforcing 指令更改为 SELINUX=disabled，保存并重启系统
离线下载软件包

yum install --downloadonly --downloaddir=/root <package-name> 

离线批量安装软件包

yum localinstall -y ./*



