一、回落终极部署（套娃方式）

配置1/配置2/实现了 vless tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出ws，回落给 trojan，由 trojan 处理后再回落给 caddy2。其应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vless+h2c+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

6、trojan+tcp+tls（tls由vless+tcp+tls提供及处理，不需配置。）

v2ray vless+tcp 类应用直连，v2ray ws 类应用分流一次；v2ray trojan+tcp 分流两次；naiveproxy 直连，v2ray h2 类应用分流（反代）一次。

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、naiveproxy（caddy2）使用本人 github 文件，可同时支持 naiveproxy、回落 h2 及 v2ray h2 反向代理。

4、caddy2 发行版不支持 PROXY protocol，如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译或选使用本人 github 文件即可。

5、v2ray v4.31.0 版本及以后才支持 trojan 及完整回落。

6、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。

二、v2ray SNI分流优化共用443端口

v2ray 通过配置相关参数对 v2ray vless+tcp、v2ray trojan+tcp、 naiveproxy(caddy2) 进行端口分流（四层转发），实现共用443端口。配置3实现了 vless tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出 ws，回落给 caddy2。同时 v2ray trojan（trojan+tcp）也以 http/1.1 或 http/2 自适应代理科学上网，回落给 caddy2。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vless+h2c+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

6、trojan+tcp+tls（回落配置。）

v2ray vless+tcp 类应用直连，v2ray ws 类应用分流一次；v2ray trojan+tcp 直连；naiveproxy 直连，v2ray h2 类应用分流（反代）一次。

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、naiveproxy（caddy2）使用本人 github 文件，可同时支持 naiveproxy、回落 h2 及 v2ray h2 反向代理。

4、v2ray v4.31.0 版本及以后才支持 trojan 及完整回落。

5、v2ray SNI分流不支持 PROXY protocol ，故配置3：没有启用 PROXY protocol，仅端口回落。
