介绍：

除 v2ray kcp 外，所用应用共用443端口。此端口由 nginx 监听（即 nginx 前置），反向代理分流出 ws。无 vless tcp 应用。v2ray 包括应用如下：

1、vless+ws+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

2、SS+v2ray-plugin+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

3、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

注意：

1、v2ray ws 类应用分流（反代）一次。

2、nginx 不支持 h2c proxy，故 nginx 不能实现 v2ray h2 反向代理。
