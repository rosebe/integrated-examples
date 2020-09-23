此配置实现 vless tcp 以http/1.1或http/2自适应代理科学上网，分流出ws，非v2ray的web回落给nginx。

利用 vless tcp 强大的回落/分流特性，实现了共用 443 端口，同时支持vless tcp与任意 ws 类应用完美共存。

注意：
nginx 支持 h2c server，但不支持http/1.1 server与h2c server共用一个端口或一个进程。
