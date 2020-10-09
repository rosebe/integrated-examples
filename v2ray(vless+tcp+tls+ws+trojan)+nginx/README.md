此配置实现 vless tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出ws，回落给 trojan，由 trojan 处理后再回落给 nginx。（套娃方式）

利用 vless 强大的回落/分流特性，实现了共用 443 端口，同时支持 vless tcp 与任意 ws 类及trojan 应用完美共存。

原理图： v2ray\trojan client <--- tcp+tls ---> v2ray server (vless+tcp+tls <- 回落 -> trojan) <-- 回落 ---> caddy2

注意：

1、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程，故回落端口或进程必须分开。

2、nginx 预编译程序包不带支持 PROXY protocol 协议的模块。如要使用此项协议应用，需加 http_realip_module 与 stream_realip_module 两模块构建自定义模板，再进行源代码编译和安装。另编译时选取源代码版本建议不要低于1.13.11。

3、v2ray v4.31.0 版本及以后才支持 trojan 及完整回落。

4、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。配置3：启用了 PROXY protocol，且进程回落。
