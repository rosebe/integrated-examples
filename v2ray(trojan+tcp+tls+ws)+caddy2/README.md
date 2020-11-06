介绍：

v2ray 前置（监听443端口），trojan+tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出 ws（WebSocket），非 v2ray 的 web 回落给 caddy2。其应用如下：

1、trojan+tcp+tls（回落/分流配置，兼容trojan。）

2、trojan+ws+tls（tls由trojan+tcp+tls提供及处理，不需配置；此配置兼容trojan-go服务端。另可改成或添加vless+ws+tls、vmess+ws+tls、SS+v2ray-plugin+tls应用。）

此配置利用 trojan+tcp 强大的回落/分流特性，实现了共用443端口，支持 trojan+tcp 与任意 ws（WebSocket） 类应用完美共存。

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan 协议。

2、trojan+ws+tls应用使用 trojan-go 客户端及 v2ray 官方客户端连接无问题，使用第三方的 v2ray 客户端基本不行。trojan-go安卓手机客户端可本人 github 中下载。

3、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

4、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

5、caddy2 发行版不支持 PROXY protocol。如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译，或下载本人 github 中编译好的 caddy2 来使用即可。

6、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
