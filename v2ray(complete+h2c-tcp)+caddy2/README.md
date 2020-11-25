介绍：

除 v2ray kcp 外，所用应用共用443端口。此端口由 caddy2 监听（即 caddy2 前置），反向代理 ws（WebSocket） 与 h2（http/2）。无 vless+tcp 应用。v2ray 包括应用如下：

1、vless+ws+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

2、vless+h2c+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

3、SS+v2ray-plugin+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

注意：

1、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray 的 h2（http/2）反向代理。

2、caddy2 的 Caddyfile 配置与 caddy.json 配置二选一（效果一样）。支持自动 https，即自动申请证书与私钥，且自动更新，http 重定向到 https。

3、nginx 不支持 h2c proxy，故不能用 nginx 来实现 v2ray 的 h2（http/2）反向代理。
