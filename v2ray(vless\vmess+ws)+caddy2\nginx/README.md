介绍：

通过 caddy2 或 nginx 前置 v2ray server 实现 ws（WebSocket） 反向代理，tls 由 caddy2 或 nginx 提供及处理。

原理图： v2ray client <------ ws+tls ------> caddy2\nginx <- ws -> v2ray server

注意：

1、此示例中若采用 caddy2 反向代理，caddyfile 配置与 caddy.json 配置二选一（效果一样）。支持自动 https，即自动申请证书与私钥，且自动更新，http 重定向到 https。

2、此示例中若采用 nginx 反向代理，如果系统版本过低，其对应发行版仓库自带 nginx 预编译程序包可能不支持 tls1.3；如需要支持 tls1.3，必须先升级 OpenSSl 版本大于 1.1.1，再进行 nginx 源代码编译和安装。
