介绍：

此配置包括 v2ray、naiveproxy(caddy2) 应用。用 haproxy 或 nginx 为 vless+tcp、trojan+tcp、naiveproxy(caddy2) 进行 SNI 分流（四层转发），实现共用443端口。另 caddy2 同时为 vless+tcp 与 trojan+tcp 提供回落服务，为 vless/vmess+h2c 提供反向代理，为 naiveproxy 提供正向代理。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、vless+h2c+tls（tls由caddy2提供及处理，，不需配置；另可改成或添加vmess+h2c+tls应用。）

4、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

6、trojan+tcp+tls（回落配置。）

v2ray vless+tcp 类应用直连，v2ray ws（WebSocket）类应用分流一次；v2ray trojan+tcp 直连；naiveproxy 直连，v2ray h2（http/2）类应用分流（反代）一次。

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan 协议。 

2、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外 caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

3、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口或一个进程（Unix Domain Socket 应用）。

4、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray 的 h2（http/2）反向代理。

5、caddy2 发行版不支持 PROXY protocol。如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译。

6、使用本人 github 中编译好的 caddy2 文件，才可同时支持 naiveproxy、h2 回落、h2（http/2）反向代理及 PROXY protocol 的应用。

7、nginx 预编译程序包不带支持 SNI 分流协议的模块。如要使用此项协议应用，需加 stream_ssl_preread_module 模块构建自定义模板，再进行源代码编译和安装。

8、配置1：没有启用 PROXY protocol，端口回落。配置2：启用了 PROXY protocol，端口回落。配置3：启用了 PROXY protocol，进程回落。
