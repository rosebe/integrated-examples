介绍：

v2ray 前置（监听443端口），trojan+tcp 以 http/1.1 代理科学上网，分流出 ws（WebSocket），非 v2ray 的 web 回落给 nginx。其应用如下：

1、trojan+tcp+tls（回落/分流配置，兼容trojan。）

2、trojan+ws+tls（tls由trojan+tcp+tls提供及处理，不需配置；此配置兼容trojan-go服务端。另可改成或添加vless+ws+tls、vmess+ws+tls、SS+v2ray-plugin+tls应用。）

此配置利用 trojan+tcp 强大的回落/分流特性，实现了共用443端口，支持 trojan+tcp 与任意 ws（WebSocket）类应用完美共存。

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan 协议。

2、trojan+ws+tls 应用使用 trojan-go 客户端及 v2ray 官方客户端连接无问题，使用第三方的 v2ray 客户端基本不行。另 trojan-go 安卓手机客户端可本人 github 中下载。

2、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程；而 v2ray 的 trojan+tcp 不支持端口或进程分离 h2 回落，故回落 nginx 只能仅采用 h1 回落；因 trojan+tcp 无 h2 连接，可能影响速度。

3、nginx 预编译程序包可能不带支持 PROXY protocol 协议的模块。如要使用此项协议应用，需加 http_realip_module（必须加） 及 stream_realip_module（可选加） 两模块构建自定义模板，再进行源代码编译和安装。另编译时选取源代码版本建议不要低于1.13.11。

4、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。配置3：启用了 PROXY protocol，且进程回落。
