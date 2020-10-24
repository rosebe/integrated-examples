介绍：

此配置包括 v2ray、naiveproxy(caddy2) 及 trojan(trojan-go) 集成。v2ray、naiveproxy(caddy2)、trojan(trojan-go) 各自公开一个监听端口，各自分别或配合提供服务。如 caddy2 还同时为 v2ray 与 trojan(trojan-go)提供回落服务。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需要另外配置；另可改成vmess+ws+tls或SS+v2ray-plugin+tls或trojan+ws+tls。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需要另外配置；另可改成vless+ws+tls或vmess+ws+tls或trojan+ws+tls。）

4、vless+h2c+tls（tls由caddy2提供及处理，不需要另外配置；另可改成vmess+h2c+tls。）

5、vmess+kcp+seed（可改成vless+kcp+seed。）

注意：

1、v2ray tcp 类应用直连，v2ray ws 类应用分流一次。

2、naiveproxy 直连。v2ray h2 类应用分流（反代）一次。

3、trojan(trojan-go) 直连。

4、naiveproxy（caddy2）使用本人 github 文件，可同时支持 naiveproxy、回落 h2 及 v2ray h2 反向代理。
