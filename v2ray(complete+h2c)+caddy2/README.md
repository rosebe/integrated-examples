介绍：

除 v2ray kcp 外，所用应用共用443端口。此端口由 v2ray 监听（即 v2ray 前置），利用 vless tcp 回落/分流特性实现，分流出 ws，其它回落给 caddy2。caddy2 再处理，h2反代，web 回落。v2ray包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vless+h2c+tls （tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

注意：

1、除 v2ray kcp 外,所用应用共用443端口。此端口由 v2ray 监听（即 v2ray 前置），利用 vless tcp 回落/分流特性实现。

2、v2ray tcp 类应用直连。v2ray ws 类应用分流（回落）一次。v2ray h2 类应用回落一次，反代（分流）一次，共计两次。

3、caddy2 等于或大于 v2.2.0-rc.1 版才支持反向代理 v2ray h2(http/2) 应用。

4、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
