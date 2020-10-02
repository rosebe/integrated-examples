此配置为v2ray新增trojan协议，目前客户端暂无，可以直接使用trojan客户端（完全兼容），以http/1.1或http/2自适应代理科学上网，web探测回落给caddy2。

注意：

1、v2ray v4.30版本及以后才支持trojan。

2、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持h2c server。

3、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。
