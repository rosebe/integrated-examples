介绍：

此配置包括v2ray回落/分流应用及v2ray h2反代应用。另v2ray包括如下应用：

包括如下应用：

1、vless+tcp+tls

2、vless+ws+tls（tls由vless+tcp+tls处理，不需要配置；另可改成vmess+ws+tls。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls处理，不需要另外配置。）

4、vless+h2 （tls由caddy2处理，不需要另外配置；另可改成vmess+h2。）

5、vmess+kcp+seed（可改成vless+kcp+seed。）

v2ray tcp 类应用直连，且以 http/1.1 或 http/2 自适应代理科学上网；v2ray ws 类应用分流；v2ray h2 应用反代。

注意：

1、除v2ray kcp外,所用应用共用443端口。此端口由v2ray监听（即v2ray前置），利用vless tcp回落/分流特性实现。

2、v2ray tcp类应用直连。v2ray ws类应用分流（回落）一次。v2ray h2类应用回落一次，反代（分流）一次，共计两次。

3、caddy2 等于或大于v2.2.0-rc.1版才支持反向代理v2ray h2(http/2) 应用。

4、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
