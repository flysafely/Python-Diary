## 安装SSR

wget --no-check-certificate https://freed.ga/github/shadowsocksR.sh; bash shadowsocksR.sh

如提示

wget :command not found
请执行

yum install wget -y
然后按提示操作。

## 一键更换内核脚本（Vultr需先执行此脚本）

wget -N --no-check-certificate https://freed.ga/kernel/ruisu.sh && bash ruisu.sh

脚本执行过程中，请勿进行任何操作。待服务器重启后，重新连接安装锐速即可。

 锐速安装脚本
wget -N --no-check-certificate https://github.com/91yun/serverspeeder/raw/master/serverspeeder.sh && bash serverspeeder.sh

若提示：The name of network interface is not eth0, please retry after changing the name.请使用备用脚本

备用脚本

wget -N --no-check-certificate https://raw.githubusercontent.com/91yun/serverspeeder/master/serverspeeder-all.sh && bash serverspeeder-all.sh
