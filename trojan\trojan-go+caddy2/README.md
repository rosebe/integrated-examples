介绍：

本配置是 trojan 或 trojan-go 应用，以 http/1.1 或 http/2 自适应代理科学上网，非trojan 或 trojan-go 的 https 的回落给 caddy2。

原理图： trojan\trojan-go client <------ https ------> trojan\trojan-go server <- web回落 -> caddy2

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、trojan-go 使用 go 实现了完全兼容 trojan，还有自己的特色。trojan-go 支持使用多路复用提升并发性能，使用路由模块实现国内直连；支持 CDN 流量中转(基于 WebSocket over TLS/SSL )；支持使用 AEAD 对 trojan 流量二次加密(基于 Shadowsocks AEAD )；支持可插拔的传输层插件，允许替换 TLS，使用其他加密隧道传输 trojan 协议流量。
