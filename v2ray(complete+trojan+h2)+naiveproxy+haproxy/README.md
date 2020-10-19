介绍：

此配置包括v2ray、naiveproxy(caddy2)应用。用haproxy或nginx为v2ray（vless+tcp+tls与trojan+tcp+tls）、naiveproxy(caddy2)进行SNI分流（四层转发），实现共用443端口。另caddy2还同时为v2ray（vless+tcp+tls与trojan+tcp+tls）提供回落服务。v2ray包括如下应用：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls处理，不需要另外配置；另可改成vmess+ws+tls。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls处理，不需要另外配置。）

4、vless+h2/h2c+tls（tls由caddy2处理，不需要另外配置；另可改成vmess+h2。）

5、vmess+kcp+seed（可改成vless+kcp+seed。）

6、trojan+tcp+tls（回落配置。）

v2ray tcp类应用直连，v2ray ws类应用分流一次；v2ray trojan直连；naiveproxy直连，v2ray h2类应用分流（反代）一次。

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、caddy2 发行版不支持 PROXY protocol，如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译或选使用本人github文件即可。

4、v2ray v4.31.0 版本及以后才支持 trojan 及完整回落。

5、用haproxy或nginx为v2ray vless+tcp、v2ray trojan、naiveproxy(caddy2)进行SNI分流（四层转发），实现共用443端口。

6、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加stream_ssl_preread_module模块构建自定义模板，再进行源代码编译和安装。

7、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
