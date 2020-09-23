此配置实现 vless tcp 以http/1.1或http/2自适应代理科学上网，分流出ws，非v2ray的web回落给caddy2。

利用 vless tcp 强大的回落/分流特性，实现了共用 443 端口，同时支持vless tcp与任意 ws 类应用完美共存。

1_v2ray_config.json为vless tcp分流vless ws 配置，2_v2ray_config.json为vless tcp分流vmess ws 配置，3_v2ray_config.json为vless tcp分流shadowsocks ws 配置。

注意：

1、caddy2 目前只能json配置才支持 h2c server，故要实现回落h2就不能采用Caddyfile配置。

2、caddy2 支持http/1.1 server与h2c server共用一个端口。
