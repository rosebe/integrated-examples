此配置实现 vless tcp 以http/1.1或http/2自适应代理科学上网，分流出ws，非v2ray的web回落给caddy2。

利用 vless tcp 强大的回落/分流特性，实现了共用 443 端口，同时支持vless tcp与任意 ws 类应用完美共存。


注意：

1、caddy2 目前只能 json 配置才支持 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、1_v2ray_config.json为vless tcp分流vless ws 配置，2_v2ray_config.json为vless tcp分流vmess ws 配置，3_v2ray_config.json为vless tcp分流shadowsocks ws 配置。
