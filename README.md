# aws_shadowsocks
aws_shadowsocks科学上网

## aws ec2 12月免费试用
aws提供12月的免费vps免费试用，直接去[AWS官网](https://aws.amazon.com/cn/)创建免费账户试用即可。

申请需要有可用的双币信用卡，过程中会刷一笔 $1 USD 的预授权，目的是验证信用卡可用，钱不是aws收走的

### 启动 ec2 实例(instance)
1. 用之前注册的aws免费账户登录[控制台](console.aws.amazon.com)，右上角选择机房位置。美国机房速度较慢，可选东京。但如果选东京，部署的shadowsocks ip也为日本，科学上网使用google/youtube等时，均默认日本网页。如果觉得不能忍，就还是用美国机房吧
2. 在aws控制台中，选择EC2，启动实例，选择Amazon Linux AMI->t2.micro(重要！small以上的不免费)，然后一路next。在最后提示需要“选择现有密钥对或创建新密钥对”时，选择差u你关键新的，然后随意命名(但也别太随意，以免后来忘记，如aws_ec2_tokoy_test)，选择下载并保存到本地
3. 绑定ip地址。依旧在控制台，左边栏选择
## shadowsocks配置
### aws服务器端
### windows客户端

## firefox+fireproxy