一、回落终极部署（套娃方式）

利用 vless 强大的回落/分流特性，实现了共用 443 端口，同时支持 vless+tcp 与任意 ws（WebSocket） 类及 trojan+tcp 应用完美共存。配置1/配置2/配置3实现了 vless+tcp 以 http/1.1 代理科学上网，分流出 ws（WebSocket）应用，回落给 trojan+tcp，trojan+tcp 处理后再回落给 nginx。其应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、trojan+tcp+tls（tls由vless+tcp+tls提供及处理，不需配置。）

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan+tcp 及完整回落。

2、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程；而 v2ray 的 trojan+tcp 不支持端口或进程分离 h2 回落，故套娃回落 nginx 只能全部采用h1回落；因vless+tcp 与 trojan+tcp 无 h2 连接，可能影响速度。

3、nginx 预编译程序包可能不带支持 PROXY protocol 协议的模块。如要使用此项协议应用，需加 http_realip_module（必须加） 及 stream_realip_module（可选加） 两模块构建自定义模板，再进行源代码编译和安装。另编译时选取源代码版本建议不要低于1.13.11。

4、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。配置3：启用了 PROXY protocol，且进程回落。

二、v2ray SNI分流优化共用443端口

v2ray 通过配置相关参数对 vless+tcp、trojan+tcp 进行端口分流（四层转发），实现共用443端口。配置4实现了 vless tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出 ws（WebSocket）应用，回落给 nginx。同时 v2ray trojan（trojan+tcp）也以 http/1.1 代理科学上网，回落给 nginx。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、trojan+tcp+tls（回落配置。）

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan+tcp 及完整回落。

2、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程；而v2ray 的 trojan+tcp 不支持端口或进程分离 h2 回落，故回落 nginx 只能仅采用 h1 回落；因  trojan+tcp 无 h2 连接，可能影响速度。

3、v2ray SNI 分流不支持 PROXY protocol ，故配置4：没有启用 PROXY protocol，仅端口回落。

三、nginx SNI分流优化共用443端口

利用 nginx 支持 SNI 分流特性，对 vless+tcp 与 trojan+tcp 进行端口分流（四层转发），实现共用443端口。配置5/配置6/配置7实现了 vless+tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出 ws（WebSocket）应用，回落给 nginx。同时 trojan+tcp 也以 http/1.1 代理科学上网，回落给 nginx。其应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、trojan+tcp+tls（回落配置。）

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan+tcp 及完整回落。

2、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程。v2ray的 trojan+tcp 不支持端口或进程分离 h2 回落，故只能采用 h1 回落；因 trojan+tcp 无 h2 连接，可能影响速度。

3、nginx 预编译程序包不带支持 SNI 分流协议的模块。如要使用此项协议应用，需加 stream_ssl_preread_module 模块构建自定义模板，再进行源代码编译和安装。

4、nginx 预编译程序包可能不带支持 PROXY protocol 协议的模块。如要使用此项协议应用，需加 http_realip_module 与 stream_realip_module 两模块构建自定义模板，再进行源代码编译和安装。另编译时选取源代码版本建议不要低于1.13.11。

5、配置5：没有启用 PROXY protocol，仅端口回落。配置6：启用了 PROXY protocol，且端口回落。配置7：启用了 PROXY protocol，且进程回落。
