介绍：

此配置包括 v2ray 与 naiveproxy 集成。除 v2ray kcp 外，所用应用共用443端口。此端口由 v2ray 监听（即 v2ray 前置），利用 vless tcp 回落/分流特性实现，分流出 ws，其它回落给 caddy2。caddy2 再处理，h2 反向代理，naiveproxy 正向代理，web 回落。包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需要另外配置；另可改成vmess+ws+tls。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需要另外配置。）

4、vless+h2c+tls（tls由vless+tcp+tls提供及处理，不需要另外配置；另可改成vmess+h2c+tls。）

5、vmess+kcp+seed（可改成vless+kcp+seed。）

6、naiveproxy （tls由vless+tcp+tls提供及处理，不需要另外配置。）

注意：

1、除 v2ray kcp 外,所用应用共用443端口。此端口由 v2ray 监听（即 v2ray 前置），利用 vless tcp 回落/分流特性实现。

2、vless tcp 以 http/1.1 或 http/2 自适应代理科学上网。利用 vless tcp 强大的回落/分流特性，还实现了 vless tcp 与任意 ws 类应用完美共存。

3、v2ray tcp 类应用直连。v2ray ws 类应用分流一次。naiveproxy 回落(分流)一次。v2ray h2 类应用回落一次，分流（反代）一次，共计两次。

4、naiveproxy（caddy2）使用本人 github 文件，可同时支持 naiveproxy、回落 h2 及 v2ray h2 反向代理。

5、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
