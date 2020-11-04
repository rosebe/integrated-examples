介绍：

本配置是 trojan 或 trojan-go 应用，非trojan 或 trojan-go 的 https 回落给 nginx。

原理图： trojan\trojan-go client <------ https ------> trojan\trojan-go server <- web回落 -> nginx

注意：

1、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口；而 trojan-go 回落，不支持回落 http/1.1 与回落 h2 端口分开。故采用 nginx 做回落服务器，trojan-go 只能 http/1.1 与 h2 二选一连接与回落。

2、trojan-go使用go实现的完整trojan代理兼容。

3、trojan-go支持使用多路复用提升并发性能，使用路由模块实现国内直连。

4、trojan-go支持CDN流量中转(基于WebSocket over TLS/SSL)。

5、trojan-go支持使用AEAD对trojan流量二次加密(基于Shadowsocks AEAD)

6、trojan-go支持可插拔的传输层插件，允许替换TLS，使用其他加密隧道传输trojan协议流量。
