介绍：

本配置是 trojan 或 trojan-go 应用，非trojan 或 trojan-go 的 http 的回落给 caddy2 或 nginx。

原理图： trojan\trojan-go client <------ https（http/1.1+tls） ------> trojan\trojan-go server <- web回落 -> caddy2\nginx

注意：

1、trojan-go使用go实现的完整trojan代理，与trojan协议以及trojan版本的配置文件格式兼容（可以直接使用trojan配置文件，但无自己特色功能了。）。

2、trojan-go支持使用多路复用提升并发性能，使用路由模块实现国内直连。

3、trojan-go支持CDN流量中转(基于WebSocket over TLS/SSL)。

4、trojan-go支持使用AEAD对trojan流量二次加密(基于Shadowsocks AEAD)

5、trojan-go支持可插拔的传输层插件，允许替换TLS，使用其他加密隧道传输trojan协议流量。
