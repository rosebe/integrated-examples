介绍：

此配置包括 v2ray、naiveproxy(caddy2) 及 trojan(trojan-go) 应用。用 haproxy 或 nginx 为 v2ray、naiveproxy(caddy2)、trojan(trojan-go) 进行 SNI 分流（四层转发），实现共用443端口。另 caddy2还同时为 v2ray 与 trojan(trojan-go) 提供回落服务。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vless+h2c+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

注意：

1、利用 vless tcp 强大的回落/分流特性，实现了 vless tcp 与任意 ws（WebSocket）类应用完美共存；且 vless tcp 以 http/1.1 或 http/2 自适应代理科学上网。

2、naiveproxy（caddy2）使用本人 github 文件，可同时支持 naiveproxy、回落 h2 及v2ray h2（http/2）反向代理。

3、naiveproxy(caddy2) 发行版不支持 PROXY protocol，如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译或选使用本人 github 文件即可。

4、用haproxy 或 nginx 为 v2ray、naiveproxy(caddy2)、trojan(trojan-go) 进行 SNI 分流（四层转发），实现共用443端口。

5、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加 stream_ssl_preread_module 模块构建自定义模板，再进行源代码编译和安装。

6、nginx 的 PROXY protocol 发送是针对共用端口全局模式，而 trojan(trojan-go) 不支持 PROXY protocol，故配置2不能用nginx SNI分流。

7、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
