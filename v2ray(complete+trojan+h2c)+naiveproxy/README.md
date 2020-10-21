介绍：

此配置包括 v2ray、naiveproxy(caddy2) 应用。v2ray、naiveproxy(caddy2) 各自公开一个监听端口，各自分别或配合提供服务。另 caddy2 还同时为v2ray（vless+tcp+tls 与 trojan+tcp+tls）提供回落服务。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需要另外配置；另可改成vmess+ws+tls。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需要另外配置。）

4、vless+h2c+tls（tls由caddy2提供及处理，不需要另外配置；另可改成vmess+h2c+tls。）

5、vmess+kcp+seed（可改成vless+kcp+seed。）

6、trojan+tcp+tls（tls由vless+tcp+tls提供及处理，不需要另外配置。）

此配置实现 vless tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出ws，回落给 trojan，由 trojan 处理后再回落给 caddy2。（套娃方式）

v2ray tcp 类应用直连，v2ray ws 类应用分流一次；v2ray trojan 分流两次；naiveproxy 直连，v2ray h2 类应用分流（反代）一次。

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、caddy2 发行版不支持 PROXY protocol，如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译或选使用本人 github 文件即可。

4、v2ray v4.31.0 版本及以后才支持 trojan 及完整回落。

5、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
