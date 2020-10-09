此配置为v2ray新增trojan协议，可以直接使用trojan客户端（完全兼容），以http/1.1或http/2自适应代理科学上网，非v2ray\trojan的web回落给caddy2。

原理图：
v2ray\trojan client <--- tcp+tls ---> v2ray server <--- web回落 ---> caddy2

注意：

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、caddy2 发行版不支持 PROXY protocol，如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译或选使用本人github文件即可。

4、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
