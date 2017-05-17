# aws_shadowsocks
aws_shadowsocks科学上网

## aws ec2 12月免费试用
aws提供12月的免费vps免费试用，直接去[AWS官网](https://aws.amazon.com/cn/)创建免费账户试用即可。

申请需要有可用的双币信用卡，过程中会刷一笔 $1 USD 的预授权，目的是验证信用卡可用，钱不是aws收走的

### 启动 ec2 实例(instance)
1. 用之前注册的aws免费账户登录[控制台](console.aws.amazon.com)，右上角选择机房位置。美国机房速度较慢，可选东京。但如果选东京，部署的shadowsocks ip也为日本，科学上网使用google/youtube等时，均默认日本网页。如果觉得不能忍，就还是用美国机房吧

2. 在aws控制台中，选择EC2，启动实例，选择Amazon Linux AMI->t2.micro(重要！small以上的不免费)，然后一路next。在最后提示需要“选择现有密钥对或创建新密钥对”时，选择创建新的，然后随意命名(但也别太随意，以免后来忘记，如aws_ec2_tokoy_test)，选择下载并保存到本地

3. 绑定ip地址。依旧在控制台，左边栏“网络与安全”下，点击“弹性ip”，选择“分配新地址”，然后就获得了一个固定ip，这个ip以后将作为登陆aws虚拟机的地址和shadowsocks服务器ip。分配完成后，选中刚才分配的ip，点击“操作”->“关联地址”，选择刚才启动的实例即可。

## shadowsocks配置
1. ssh登陆aws虚拟机: 依旧在aws EC2 控制控制台下，点击“连接”，按照提示，修改刚才下载到本地的密钥对文件权限。然后 ssh 连接即可
2. 安装shadowsocks：登陆虚拟机后，按照如下安装shadowsocks
``` shell
$ wget --no-check-certificate https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh 
$ chmod +x shadowsocks.sh
$ sudo ./shadowsocks.sh 2>&1 | tee shadowsocks.log
```
如果提示 `https://raw.githubusercontent.com/teddysun/shadowsocks_install/master/shadowsocks.sh` 无法访问(404)，直接去[Teddysun/shadowsocks_install
](https://github.com/teddysun/shadowsocks_install/) 找 `shadowsocks.sh` 的url，替换上面即可

shadowsocks安装过程中，会要求输入默认密码和端口，按自己需要输入即可，但记得保留。这是之后使用代理需要用到的

如一切正常，最后命令行提示`Congratulations, shadowsocks server install completed!`，同时ss的server ip/port 和密码都会再显示

最后编辑 `/etc/shadowsocks.json`，修改`server`字段为`"server"="0.0.0.0"`，再启动ss `$ sudo /etc/init.d/shadowsocks start`，shadowsocks配置就完成了

### aws服务器端
1. 修改aws服务器端开放的端口。在aws控制台，点击刚才启动实例的安全组，在“入站”中，点击编辑，添加自定义的 TCP 和 UDP 规则，端口为`8989`（或自己设置的ss端口），来源选择任何位置或者自定义ip
2. 以上，aws ec2 服务器设置和shadowsocks配置均已完成
### windows客户端
1. windows下，去[shadowsocks](https://github.com/shadowsocks/shadowsocks-windows)下载最新的release客户端，按照说明配置即可
## firefox+fireproxy
1. firefox下，建议配合 fireproxy 使用，毕竟国内网站并不需要代理。配置代理规则时，可订阅[gfwlist](https://github.com/gfwlist/gfwlist)

## 祝翻墙愉快！
