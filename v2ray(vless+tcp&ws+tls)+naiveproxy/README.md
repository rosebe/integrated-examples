介绍：

v2ray 前置（监听443端口），利用 vless+tcp 强大的回落/分流特性，实现了共用443端口。vless+tcp 以 h2 或 http/1.1 自适应协商连接，分流 ws（WebSocket）连接，非 v2ray 的连接回落给 caddy2；caddy2 再处理，对 naiveproxy 进行正向代理。其应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、naiveproxy （tls由vless+tcp+tls提供及处理，不需配置。）

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口或一个进程（Unix Domain Socket 应用）。

3、使用本人 github 中编译好的 caddy2 文件，才支持 naiveproxy 及 PROXY protocol 应用。

4、配置1：没有启用 PROXY protocol，端口回落。配置2：没有启用 PROXY protocol，进程回落。配置3：启用了 PROXY protocol，进程回落。
