介绍：

此配置实现了 v2ray 前置（监听443端口），vless+tcp 以 http/2 或 http/1.1 自适应代理科学上网，非 v2ray 的 web 回落给 caddy2。

原理图：
v2ray client <------ tcp+tls ------> v2ray server <- web回落 -> caddy2

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、caddy2 发行版不支持 PROXY protocol。如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译，或下载本人 github 中编译好的 caddy2 来使用即可。

4、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
