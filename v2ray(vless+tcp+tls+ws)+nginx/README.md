介绍：

此配置实现 vless tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出 ws（WebSocket），非 v2ray 的 web 回落给 nginx。其应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

利用 vless tcp 强大的回落/分流特性，实现了共用443端口，同时支持 vless tcp 与任意 ws 类应用完美共存。

注意：

1、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程，故回落端口或进程必须分开。

2、nginx 预编译程序包可能不带支持 PROXY protocol 协议的模块。如要使用此项协议应用，需加 http_realip_module（必须加的） 及 stream_realip_module（可选加） 两模块构建自定义模板，再进行源代码编译和安装。另编译时选取源代码版本建议不要低于1.13.11。

3、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。配置3：启用了 PROXY protocol，且进程回落。

