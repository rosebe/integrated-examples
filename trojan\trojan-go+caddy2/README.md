介绍：

本配置是 trojan 或 trojan-go 应用，非trojan 或 trojan-go 的 https 的回落给 caddy2。

原理图： trojan\trojan-go client <------ https ------> trojan\trojan-go server <- web回落 -> caddy2

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、trojan-go使用go实现的完整trojan代理兼容。

4、trojan-go支持使用多路复用提升并发性能，使用路由模块实现国内直连。

5、trojan-go支持CDN流量中转(基于WebSocket over TLS/SSL)。

6、trojan-go支持使用AEAD对trojan流量二次加密(基于Shadowsocks AEAD)

7、trojan-go支持可插拔的传输层插件，允许替换TLS，使用其他加密隧道传输trojan协议流量。
