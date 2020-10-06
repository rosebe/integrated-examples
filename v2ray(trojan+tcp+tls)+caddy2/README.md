此配置为v2ray新增trojan协议，可以直接使用trojan客户端（完全兼容），以http/1.1或http/2自适应代理科学上网，非v2ray\trojan的web回落给caddy2。

原理图：
v2ray\trojan client <--- tcp+tls ---> v2ray server <--- web回落 ---> caddy2

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持h2c server。caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

2、v2ray v4.30 版本及以后才支持 trojan 。另外 trojan 回落还很简易（以后版本可能改进成vless+tcp回落模式。），如设置连接配置h2与http/1.1同时支持，回落流也是h2与http/1.1复合的，暂不支持分开回落，故目前只有 caddy2 支持。
