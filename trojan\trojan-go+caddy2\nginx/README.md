介绍：

本配置是 trojan 或 trojan-go 应用，非trojan 或 trojan-go 应用回落给 caddy2 或 nginx。

原理图： trojan\trojan-go client <------ https ------> trojan\trojan-go server <- web回落 -> caddy2\nginx

注意：

1、trojan-go使用Go实现的完整Trojan代理，与Trojan协议以及Trojan版本的配置文件格式兼容。安全，高效，轻巧，易用。

2、trojan-go支持使用多路复用提升并发性能，使用路由模块实现国内直连。

3、trojan-go支持CDN流量中转(基于WebSocket over TLS/SSL)。

4、trojan-go支持使用AEAD对Trojan流量二次加密(基于Shadowsocks AEAD)

5、trojan-go支持可插拔的传输层插件，允许替换TLS，使用其他加密隧道传输Trojan协议流量。
