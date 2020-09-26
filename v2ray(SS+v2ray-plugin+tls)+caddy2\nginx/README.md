本配置采用 v2ray 自带 shadowsocks 协议及自身 v2ray '分离'出的 v2ray-plugin 插件，直接实现 shadowsocks+v2ray-plugin 应用，客户端直接使用 shadowsocks 即可。

另外通过 caddy2 或 nginx 前置 v2ray server 实现 ws 反向代理。

原理图： v2ray client <----- ws+tls ------> caddy2\nginx <- ws -> v2ray server
