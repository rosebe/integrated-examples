介绍：

此配置为v2ray新增trojan协议。可以直接使用trojan客户端（完全兼容），以http/1.1代理科学上网，非v2ray\trojan的web回落给nginx。

原理图： v2ray\trojan client <------ tcp+tls ------> v2ray server <- web回落 -> nginx

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan 及完整回落。

2、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程；而v2ray的trojan不支持端口或进程分离h2回落，故回落nginx只能仅采用h1回落。

3、nginx 预编译程序包不带支持 PROXY protocol 协议的模块。如要使用此项协议应用，需加 http_realip_module 与 stream_realip_module 两模块构建自定义模板，再进行源代码编译和安装。另编译时选取源代码版本建议不要低于1.13.11。

4、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。配置3：启用了 PROXY protocol，且进程回落。
