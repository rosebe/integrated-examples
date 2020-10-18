介绍：

除 v2ray kcp 外，所用应用共用443端口。此端口由 v2ray 监听（即 v2ray 前置），利用 vless tcp 回落/分流特性实现，分流出 ws，其它回落给 caddy2。caddy2再处理，h2反代，web回落。包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls处理，不需要另外配置；另可改成vmess+ws+tls。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls处理，不需要另外配置。）

4、vless+h2 （tls由vless+tcp+tls处理，不需要另外配置；另可改成vmess+h2。）

5、vmess+kcp+seed（可改成vless+kcp+seed。）

注意：

1、除v2ray kcp外,所用应用共用443端口。此端口由v2ray监听（即v2ray前置），利用vless tcp回落/分流特性实现。

2、v2ray tcp类应用直连。v2ray ws类应用分流（回落）一次。v2ray h2类应用回落一次，反代（分流）一次，共计两次。

3、caddy2 等于或大于v2.2.0-rc.1版才支持反向代理v2ray h2(http/2) 应用。

4、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
