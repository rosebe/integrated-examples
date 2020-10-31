一、回落终极部署（套娃方式）

利用 vless 强大的回落/分流特性，实现了共用 443 端口，同时支持 vless+tcp 与任意 ws（WebSocket）类及 trojan+tcp 应用完美共存。配置1/配置2/实现了 vless+tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出 ws（WebSocket），回落给 trojan+tcp，trojan+tcp 处理后再回落给 caddy2。其应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、trojan+tcp+tls（tls由vless+tcp+tls提供及处理，不需配置。）

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、caddy2 发行版不支持 PROXY protocol。如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译；或下载本人 github 中编译好的 caddy2 来使用即可。

4、v2ray v4.31.0 版本及以后才支持 trojan+tcp 及完整回落。

5、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。

二、v2ray SNI 分流优化共用443端口

v2ray 通过配置相关参数对 vless+tcp、trojan+tcp 进行端口分流（四层转发），实现共用443端口。配置3实现了 vless+tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出 ws（WebSocket），回落给 caddy2。同时 trojan+tcp 也以 http/1.1 或 http/2 自适应代理科学上网，回落给 caddy2。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、trojan+tcp+tls（回落配置。）

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外 caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、v2ray v4.31.0 版本及以后才支持 trojan+tcp 及完整回落。

4、v2ray SNI分流不支持 PROXY protocol ，故配置3：没有启用 PROXY protocol，仅端口回落。
