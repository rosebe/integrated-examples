介绍：

此配置为 v2ray 新增 trojan 协议，以 tcp 方式传输，实现了兼容 trojan，即可直接使用 trojan 客户端连接。

另外也实现了以 http/1.1 或 http/2 自适应代理科学上网，非 v2ray\trojan 的 web 回落给 caddy2。

原理图：
v2ray\trojan client <------ tcp+tls ------> v2ray server <- web回落 -> caddy2

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、caddy2 发行版不支持 PROXY protocol。如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译，或下载本人 github 中编译好的 caddy2 来使用即可。

4、v2ray v4.31.0 版本及以后才支持 trojan+tcp 及完整回落。 

5、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
