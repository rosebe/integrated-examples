介绍：

此配置包括v2ray、naiveproxy及trojan(trojan-go)集成。v2ray、naiveproxy(caddy2)、trojan(trojan-go)各自公开一个监听端口，各自分别或配合提供服务。如caddy2还同时为v2ray与trojan(trojan-go)提供回落服务。v2ray包括如下应用：

1、vless+tcp+tls

2、vless+ws+tls（tls由vless+tcp+tls处理，不需要配置；另可改成vmess+ws+tls。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls处理，不需要另外配置。）

4、vless+h2 （tls由caddy2处理，不需要另外配置；另可改成vmess+h2。）

5、vmess+kcp+seed（可改成vless+kcp+seed。）

注意：

1、v2ray tcp类应用直连，v2ray ws类应用分流一次。

2、naiveproxy直连。v2ray h2类应用分流（反代）一次。

3、trojan(trojan-go)直连。

4、naiveproxy（caddy2）使用本人github文件，可同时支持naiveproxy、回落 h2 及v2ray h2反向代理。

5、caddy2 发行版不支持 PROXY protocol，如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译或选使用本人github文件即可。

6、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
