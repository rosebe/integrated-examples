介绍：

此配置包括 v2ray、naiveproxy(caddy2) 及 trojan(trojan-go) 应用。用 haproxy 或 nginx 为 v2ray、naiveproxy(caddy2)、trojan(trojan-go) 进行 SNI 分流（四层转发），实现共用443端口。另 caddy2 还同时为 vless+tcp 与 trojan(trojan-go) 提供回落服务，为 vless/vmess+h2c 提供反向代理，为 naiveproxy 提供正向代理。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、vless+h2c+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

4、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray 的 h2（http/2）反向代理。

4、caddy2 发行版不支持 PROXY protocol。如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译。

5、使用本人 github 中编译好的 caddy2 文件，才可同时支持 naiveproxy、h2 回落、h2（http/2）反向代理及 PROXY protocol的应用。

6、nginx 预编译程序包一般不带支持 SNI 分流协议的模块。如要使用此项协议应用，需加 stream_ssl_preread_module 模块构建自定义模板，再进行源代码编译和安装。

7、nginx SNI 中的 PROXY protocol 发送是针对共用端口全局模式，而 trojan(trojan-go) 不支持 PROXY protocol，故配置2不能用 nginx SNI 分流。

8、因 caddy2 同时为 vless+tcp 与 trojan(trojan-go) 提供回落服务，且 trojan(trojan-go) 不支持 PROXY protocol，故 caddy2 的 web 回落不能启用 PROXY protocol 接收，从而 vless+tcp 的 web 回落部分也不能启用 PROXY protocol 发送。

9、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用 PROXY protocol（除 web 回落部分外），且端口回落。
