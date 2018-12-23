限Centos7！不支持OVZ。

据称相比原版BBR，改善了一些。原版BBR一键安装：TCP加速：BBR 一键安装

一、CentOS 7下一键安装BBR修正版脚本（自动安装内核并启用）：

wget -N --no-check-certificate "https://github.com/cx9208/bbrplus/raw/master/ok_bbrplus_centos.sh" && chmod +x ok_bbrplus_centos.sh && ./ok_bbrplus_centos.sh

安装后，执行uname -r，显示 4.14.89 则切换内核成功

执行lsmod | grep bbr，显示有 bbrplus 则开启成功

二、CentOS 7手动安装BBR修正版

下载内核
wget --no-check-certificate https://github.com/cx9208/bbrplus/raw/master/centos/x86_64/kernel-4.14.89-1.x86_64.rpm

安装
yum install -y kernel-4.14.89-1.x86_64.rpm

切换启动内核

grub2-set-default 'CentOS Linux (4.14.89) 7 (Core)'

启用
echo "net.core.default_qdisc=fq" >> /etc/sysctl.conf

echo "net.ipv4.tcp_congestion_control=bbrplus" >> /etc/sysctl.conf

最后重启
reboot
