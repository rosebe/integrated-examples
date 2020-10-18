介绍：

此配置包括v2ray与naiveproxy集成。除 v2ray kcp 外，所用应用共用443端口。此端口由 v2ray 监听（即 v2ray 前置），利用 vless tcp 回落/分流特性实现，分流出 ws，其它回落给 caddy2。caddy2再处理，h2反向代理，naiveproxy正向代理，web回落。包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls处理，不需要配置；另可改成vmess+ws+tls。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls处理，不需要另外配置。）

4、vless+h2 （tls由vless+tcp+tls处理，不需要另外配置；另可改成vmess+h2。）

5、vmess+kcp+seed（可改成vless+kcp+seed。）

6、naiveproxy （tls由vless+tcp+tls处理，不需要另外配置。）

注意：

1、除v2ray kcp外,所用应用共用443端口。此端口由v2ray监听（即v2ray前置），利用vless tcp回落/分流特性实现。

2、vless tcp 以http/1.1或http/2自适应代理科学上网。利用 vless tcp 强大的回落/分流特性，还实现了vless tcp与任意 ws 类应用完美共存。

3、v2ray tcp类应用直连。v2ray ws类应用分流一次。naiveproxy回落(分流)一次。v2ray h2类应用回落一次，分流（反代）一次，共计两次。

4、naiveproxy（caddy2）使用本人github文件，可同时支持naiveproxy、回落 h2 及v2ray h2反向代理。

5、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
