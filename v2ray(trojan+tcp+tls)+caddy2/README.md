介绍：

v2ray 前置（监听443端口），trojan+tcp 以 h2 或 http/1.1 自适应协商连接，非 v2ray\trojan 的 web 连接回落给 caddy2。

原理图：v2ray\trojan client <------ tcp+tls ------> v2ray server <- web回落 -> caddy2

此配置为 v2ray 新增 trojan 协议，以 tcp 方式传输，实现了兼容 trojan，即可直接使用 trojan 客户端连接。

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan 协议。 

2、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

3、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口或一个进程（Unix Domain Socket 应用）。

4、caddy2 发行版不支持 PROXY protocol（接收）。如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译，或下载本人 github 中编译好的 caddy2 来使用即可。

5、配置1：全部没有启用 PROXY protocol，端口回落。配置2：仅回落没有启用 PROXY protocol，进程回落。配置3：全部启用了 PROXY protocol，进程回落。
