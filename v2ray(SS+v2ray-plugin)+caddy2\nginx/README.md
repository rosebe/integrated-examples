介绍：

本配置采用 v2ray 自带 shadowsocks 协议及自身 v2ray ‘分离’ 出的 v2ray-plugin 插件，直接实现 shadowsocks 加 v2ray-plugin 插件的 ws(WebSocket) 应用，客户端直接使用 shadowsocks 即可。

另外通过 caddy2 或 nginx 前置 v2ray server 实现 ws 反向代理，tls 由 caddy2 或 nginx 提供及处理。

原理图： shadowsocks client <------ ws+tls ------> caddy2\nginx <- ws -> v2ray server

注意：

1、v2ray_domainsocket_config.json仅适用linux服务器，但效率高；而v2ray_redirect_config.json可以适用全部服务器，但效率稍低。

2、若系统版本过低，其对应发行版仓库自带 nginx 预编译程序包可能不支持 tls1.3；如需要支持 tls1.3，必须先升级 OpenSSl 版本大于 1.1.1，再进行 nginx 源代码编译和安装。

3、v2ray中shadowsocks+v2ray-plugin 插件的 ws(WebSocket) 应用不等于shadowsocks+WebSocket，两者不兼容，它仅兼容shadowsocks（客户端）+v2ray-plugin（插件）。
