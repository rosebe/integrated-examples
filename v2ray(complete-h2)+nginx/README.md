除 v2ray kcp 外,所用应用共用443端口。此端口由 v2ray 监听（即 v2ray 前置），利用 vless tcp 回落/分流特性实现，分流出 ws，非 v2ray 的 web 回落给 nginx。

v2ray tcp 类应用直连，且以 http/1.1 或 http/2 自适应代理科学上网；v2ray ws 类应用分流一次。

注意：

1、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程，故回落端口或进程必须分开。

2、nginx 不支持 h2c proxy，故无法搭建 vless\vmess+h2 反代应用。

3、nginx 预编译程序包不带支持 PROXY protocol 协议的模块。如要使用此项协议应用，需加 http_realip_module 与 stream_realip_module 两模块构建自定义模板，再进行源代码编译和安装。另编译时选取源代码版本建议不要低于1.13.11。

4、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。配置3：启用了 PROXY protocol，且进程回落。
