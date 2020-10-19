介绍：

除 v2ray kcp 外，所用应用共用443端口。此端口由 caddy2 监听（即 caddy2 前置），反向代理分流 ws 与 h2。无 vless tcp 应用。包括应用如下：

1、vless+ws+tls（tls由caddy2处理，不需要另外配置；另可改成vmess+ws+tls。）

2、SS+v2ray-plugin+tls（tls由caddy2处理，不需要另外配置。）

3、vless+h2c+tls（tls由caddy2处理，不需要另外配置；另可改成vmess+h2c。）

4、vmess+kcp+seed（可改成vless+kcp+seed。）

注意：

1、v2ray ws 类应用分流（反代）一次。v2ray h2 类应用分流（反代）一次。

2、caddy2 等于或大于 v2.2.0-rc.1 版才支持反向代理 v2ray h2(http/2) 应用。
