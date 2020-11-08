一、流量统计介绍

流量统计需消耗资源，严重时可影响速度。非必要不必配置，且此流量统计配置，不支持重启及修改配置后，保持之前流量统计记录。

二、此配置可以统计情况

1、入站的统计，需要根据 tag 来记录入站流量。

2、用户的统计，依据 email 区分。socks, shadowsocks, http 等其他协议内的用户不支持被统计。  

三、要实现流量统计功能，配置内需要确保存在以下配置：

1、"stats":{} 对象的存在

2、"api" 配置对象里面有 StatsService

3、"policy" 中的统计开关为 true，除了各个用户的统计，还有全局统计

4、clients 里面要有 email

5、专用的 dokodemo-door 协议的入口，tag 为 api

6、routing 里面有 inboundTag:api -> outboundTag:api 的规则 

四、流量信息的处理

1、把 traffic.sh 脚本上传到服务器 root 目录，并授予执行权限。另外注意调整修改 _APISERVER 一行的连接具体的端口参数。

2、执行 ./traffic.sh 即可查看流量统计。
