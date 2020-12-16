一、回落终极部署（配置1/配置2/配置3套娃方式）

v2ray 前置（监听443端口），vless+tcp 以 h2 或 http/1.1 自适应协商连接，分流 ws（WebSocket）连接，回落给 trojan+tcp，trojan+tcp 处理后再回落给 caddy2。其应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、trojan+tcp+tls（tls由vless+tcp+tls提供及处理，不需配置。）

利用 vless 强大的回落/分流特性，实现了共用 443 端口，支持 vless+tcp 与任意 ws（WebSocket）类及 trojan+tcp 应用完美共存。

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan 协议。 

2、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

3、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

4、caddy2 发行版不支持 PROXY protocol。如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译；或下载本人 github 中编译好的 caddy2 来使用即可。

5、配置1：caddy2 没有启用 PROXY protocol，仅端口回落。配置2：caddy2 没有启用 PROXY protocol，仅进程回落。配置3：caddy2 启用了 PROXY protocol，且进程回落。

二、v2ray SNI 分流优化共用443端口（配置4/配置5）

v2ray 通过配置相关参数对 vless+tcp、trojan+tcp 进行端口分流（四层转发），实现共用443端口。vless+tcp 以 h2 或 http/1.1 自适应协商连接，分流 ws（WebSocket）连接，非 v2ray 的 web 连接回落给 caddy2。trojan+tcp 也以 h2 或 http/1.1 自适应协商连接，非 v2ray 的 web 连接也回落给 caddy2。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、trojan+tcp+tls（回落配置。）

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan 协议。 

2、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外 caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

3、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

4、v2ray SNI 分流不支持 PROXY protocol（发送），故配置4：caddy2 没有启用 PROXY protocol，仅端口回落；配置5：caddy2 没有启用 PROXY protocol，仅进程回落。
