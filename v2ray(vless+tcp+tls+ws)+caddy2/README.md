此配置实现 vless tcp 以http/1.1或http/2自适应代理科学上网，分流出ws，非v2ray的web回落给caddy2。

利用 vless tcp 强大的回落/分流特性，实现了共用 443 端口，同时支持vless tcp与任意 ws 类应用完美共存。

1_v2ray_config.json为VLESS TCP分流VLESS WS 配置，2_v2ray_config.json为VLESS TCP分流VMess WS 配置，3_v2ray_config.json为VLESS TCP分流shadowsocks WS 配置。
