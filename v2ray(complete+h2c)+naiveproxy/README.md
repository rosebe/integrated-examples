介绍：

此配置包括 v2ray 与 naiveproxy 集成。除 v2ray kcp 外，所用应用共用443端口。此端口由 v2ray 监听（即 v2ray 前置），利用 vless+tcp 回落/分流特性实现，分流出 ws（WebSocket），其它回落给 caddy2。caddy2 再处理，发现vless/vmess+h2c就执行反向代理，发现 naiveproxy 就执行正向代理。包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vless+h2c+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

6、naiveproxy （tls由vless+tcp+tls提供及处理，不需配置。）

注意：

1、v2ray tcp 类应用直连。v2ray ws 类应用分流一次。naiveproxy 回落(分流)一次。v2ray h2 类应用回落一次，分流（反代）一次，共计两次。

2、1、naiveproxy（caddy2）使用本人 github 中编译好的 caddy2 文件，可同时支持 naiveproxy、h2 回落 、vless/vmess+h2c 反向代理及 PROXY protocol的应用。

3、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
