这里是主流科学上网的优化配置示例。如是不太了解科学上网，建议先依次从简单到复杂参考及部署。

单一应用服务器端配置示例  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1、v2ray(vless\vmess+kcp+seed) （若网络极差，推荐部署。）  
2、v2ray(vless\vmess+ws)+caddy2\nginx （WebSocket的caddy2或nginx反向代理，之前推荐部署。）  
3、v2ray(vless\vmess+h2c)+caddy2 （http/2的caddy2反向代理。）  
4、v2ray(SS+v2ray-plugin)+caddy2\nginx （兼容shadowsocks的WebSocket应用，caddy2或nginx反向代理。）  
5、v2ray(vless+tcp+tls)+caddy2 （以h2或http/1.1任意连接实现代理，回落给caddy2。）  
6、v2ray(vless+tcp+tls)+nginx （以h2或http/1.1任意连接实现代理，回落给nginx。）  
7、v2ray(trojan+tcp+tls)+caddy2 （兼容trojan应用，以h2或http/1.1任意连接实现代理，回落给caddy2。）  
8、v2ray(trojan+tcp+tls)+nginx （兼容trojan应用，以h2或http/1.1连接实现代理，回落给nginx。）  
9、v2ray(trojan+ws)+caddy2\nginx （兼容trojan-go的WebSocket应用，caddy2或nginx反向代理。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1、trojan\trojan-go+caddy2 （trojan或trojan-go应用，以h2或http/1.1任意连接实现代理，回落给caddy2。）  
2、trojan\trojan-go+nginx （trojan或trojan-go应用，以h2或http/1.1连接实现代理，回落给nginx。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1、naiveproxy(caddy2+forwardproxy) （naiveproxy应用，以http/2或http/3代理。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  

综合应用服务器端配置示例  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1、v2ray为主、caddy2为辅及其它应用。  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(complete+h2c-tcp)+caddy2 （caddy2前置，反向代理WebSocket与http/2的综合应用；之前推荐部署。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(vless+tcp&ws+tls)+caddy2 （目前推荐部署，同时支持vless+tcp与WebSocket类应用，回落给caddy2。）  
2）、v2ray(complete+h2c)+caddy2 （v2ray综合应用+反向代理http/2应用。）  
3）、v2ray(complete+h2c)+naiveproxy （上一项应用+naiveproxy应用。）  
4）、v2ray(complete+h2c)+naiveproxy+trojan （上一项应用+trojan应用及共用端口。）  
5）、v2ray(complete+h2c)+naiveproxy+trojan+haproxy （用haproxy对上一项应用进行SNI分流，共用端口。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(vless&trojan+tcp&ws+tls)+caddy2 （回落终极部署/套娃方式，或共用端口。）  
2）、v2ray(complete+trojan+h2c)+naiveproxy （v2ray全部应用+naiveproxy应用及共用端口。）  
3）、v2ray(complete+trojan+h2c)+naiveproxy+haproxy （用haproxy对上一项应用进行SNI分流，共用端口。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
2、v2ray为主、nginx为辅及其它应用。  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(complete-tcp)+nginx （nginx前置，反向代理WebSocket的综合应用；之前推荐部署。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(vless+tcp&ws+tls)+nginx （目前推荐部署，同时支持vless+tcp与WebSocket类应用，回落给nginx。）  
2）、v2ray(complete)+nginx （v2ray综合应用。）  
3）、v2ray(complete)+nginx+trojan （上一项应用+trojan应用及共用端口。）  
4）、v2ray(complete+h2c)+nginx+trojan+naiveproxy （上一项应用+naiveproxy+反向代理http/2应用及共用端口。）  
+++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1）、v2ray(vless&trojan+tcp&ws+tls)+nginx （回落终极部署/套娃方式，或共用端口。）  
2）、v2ray(complete+trojan+h2c)+nginx+naiveproxy （v2ray全部应用+naiveproxy应用及共用端口。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
注意：  
1、naiveproxy=caddy2+forwardproxy。此程序文件已编译好，本github下载即可。  
2、complete表示包含v2ray的vless+tcp+tls、vless+ws+tls、SS+v2ray-plugin+tls、vmess+kcp+seed的综合应用。  
3、所有配置文件都配置了禁用BT。如不需要，可以删除相关配置（参考v2ray(other configuration)中BT_config.json文件）。  
4、v2ray从版本v4.33.0删除了xtls应用，故若还想用xtls应用，请选Xray。Xray是v2ray分支，也是因为这个应用分家。另外配置示例的log部分，注意修改对应v2ray或xray。
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  

特殊应用服务器端配置示例  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  
1、v2ray(other configuration) （v2ray禁用BT的配置方法、v2ray SNI分流的配置方法、v2ray流量统计的配置方法。）  
2、caddy2(other configuration) （分别回落caddy2不同网站的配置方法。）  
3、nginx(other configuration) （nginx SNI分流v2ray回落应用与网站应用的配置方法。）  
++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++++  

client configuration  
官方客户端文本配置示例目录，目录内包含对应服务端应用的官方客户端文本配置示例。（使用图形界面客户端仅参考即可）

service configuration  
程序service文件目录，目录内包含各个程序service配置示例。（手工配置程序由操作系统管理及自动运行可参考）

使用/贡献指南  
1、若程序增加新功能，开始在单一应用服务器端配置示例中添加；过一段时间稳定后才会综合应用服务器端配置示例中添加。如除trojan+tcp套娃外，vless+tcp及trojan+tcp的xtls已全部加上。  
2、欢迎你提交 PR ,如对现行配置示例优化修订，或将自己使用的配置制作模板提交等。
