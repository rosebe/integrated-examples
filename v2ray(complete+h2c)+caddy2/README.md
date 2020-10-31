介绍：

除 v2ray kcp 外，所用应用共用443端口。此端口由 v2ray 监听（即 v2ray 前置），利用 vless+tcp 回落/分流特性实现，分流出 ws（WebSocket），其它回落给 caddy2。caddy2 再处理，对 vless/vmess+h2c 提供反向代理。v2ray包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vless+h2c+tls （tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

v2ray tcp 类应用直连。v2ray ws（WebSocket）类应用分流（回落）一次。v2ray h2（http/2）类应用回落一次，反代（分流）一次，共计两次

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray 的 h2（http/2）反向代理。

4、caddy2 发行版不支持 PROXY protocol。如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译，或下载本人 github 中编译好的 caddy2 来使用即可。

5、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
