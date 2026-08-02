# centos7-core
centos 7最后的内核 此内核支持bbr

# 1. 导入 GPG 密钥
rpm --import https://www.elrepo.org/RPM-GPG-KEY-elrepo.org
rpm --import https://www.elrepo.org/RPM-GPG-KEY-v2-elrepo.org

# 2. 下载
cd /tmp
wget http://mirrors.coreix.net/elrepo-archive-archive/kernel/el7/x86_64/RPMS/kernel-lt-5.4.278-1.el7.elrepo.x86_64.rpm

本厂库保存了下载到的最后的内核文件

# 3. 校验（必须看到 OK 才继续）
rpmkeys -K kernel-lt-5.4.278-1.el7.elrepo.x86_64.rpm

# 4. 安装（保留旧内核）
rpm -ivh kernel-lt-5.4.278-1.el7.elrepo.x86_64.rpm

# 查看内核
awk -F\' '$1=="menuentry " {print i++ " : " $2}' /etc/grub2.cfg

# 5. 设置默认启动
grub2-set-default 0
grub2-mkconfig -o /boot/grub2/grub.cfg

# 6. 重启验证
reboot