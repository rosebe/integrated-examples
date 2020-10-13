这里是主流科学上网的优化集成配置示例。如是不太了解科学上网，建议先依次从简单到复杂参考及部署。

单一应用集成服务器端配置示例  
1、v2ray(vless\vmess+ws+tls)+caddy2\nginx （之前vmess协议时代，推荐部署。）  
2、v2ray(vless\vmess+h2)+caddy2 （h2优势：链路复用。）  
3、v2ray(SS+v2ray-plugin+tls)+caddy2\nginx（不常用，如需直接使用shadowsocks客户端可部署。）  
4、v2ray(vless+tcp+tls)+caddy2 （回落给caddy2，支持http/1.1与h2回落。）  
5、v2ray(trojan+tcp+tls)+caddy2 （新增trojan协议应用，http/1.1与h2回落给caddy2。）  
6、v2ray(vless+tcp+tls)+nginx （回落给nginx，支持http/1.1与h2回落。）  
7、v2ray(trojan+tcp+tls)+nginx （新增trojan协议应用，http/1.1与h2回落给nginx。）  

综合应用集成服务器端配置示例  
1、v2ray为主，caddy2为辅。  
1）、v2ray(complete+h2-tcp)+caddy2 （caddy2前置，主要反代ws与h2的综合应用。）  
2）、v2ray(vless+tcp+tls+ws)+caddy2 （目前推荐部署，同时支持tcp与ws，回落给caddy2。）  
3）、v2ray(complete+h2)+caddy2 （v2ray综合应用+反代h2应用。）  
4）、v2ray(complete+h2)+naiveproxy （上一项应用+naiveproxy应用。）  
5）、v2ray(complete+h2)+naiveproxy+trojan（上一项应用+trojan应用。各程序监听端口对外公开，同级对等。）  
6）、v2ray(complete+h2)+naiveproxy+trojan+haproxy （用haproxy对上一项应用进行SNI分流，共用443端口。）  
7）、v2ray(vless+tcp+tls+ws+trojan)+caddy2 （回落终极部署，同时支持tcp与ws及trojan，回落给caddy2。）  
8）、v2ray(complete+trojan+h2)+naiveproxy （上一项应用融合v2ray全部应用+naiveproxy应用。各程序监听端口对外公开，同级对等。）  
9）、v2ray(complete+trojan+h2)+naiveproxy+haproxy （用haproxy对上一项应用进行SNI分流，共用443端口。）  
2、v2ray为主，nginx为辅。  
1）、v2ray(vless+tcp+tls+ws)+nginx （目前推荐部署，同时支持tcp与ws，回落给nginx。）  
2）、v2ray(complete)+nginx （v2ray综合应用。）  
3）、v2ray(complete)+nginx+trojan（上一项应用+trojan应用。可用nginx进行SNI分流，共用443端口。）  
4）、v2ray(complete+h2)+nginx+trojan+naiveproxy （上一项应用+naiveproxy及反代h2应用。可用nginx进行SNI分流，共用443端口。）  
5）、v2ray(vless+tcp+tls+ws+trojan)+nginx （回落终极部署或nginx SNI分流优化，同时支持tcp与ws及trojan，回落给nginx。）  
6）、v2ray(complete+trojan+h2)+nginx+naiveproxy （上一项应用融合v2ray全部应用+naiveproxy应用。可用nginx进行SNI分流，共用443端口。）  
注意：  
1、naiveproxy=caddy2+forwardproxy。此程序文件已编译好，本github下载即可。  
2、complete表示包含v2ray的vless+tcp+tls、vless\vmess+ws+tls、SS+v2ray-plugin+tls、vmess+kcp+seed的综合应用。  

service  
各程序service文件目录

client  
各客户端配置示例目录

使用/贡献指南  
1、若程序增加新功能（如vless+tcp的xtls），开始主要单一应用集成服务器端配置示例中添加；过一段时间稳定后才会全部配置示例中添加。  
2、欢迎你提交 PR ,如对现行配置示例优化修订，或将自己使用的配置制作模板提交等。
