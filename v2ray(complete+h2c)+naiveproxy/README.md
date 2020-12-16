介绍：

此配置包括 v2ray 与 naiveproxy 集成。除 v2ray kcp 外，所用应用共用443端口。此端口由 v2ray 监听（即 v2ray 前置），利用 vless+tcp 回落/分流特性实现，分流出 ws（WebSocket）连接，其它连接回落给 caddy2；caddy2 再处理，对 vless/vmess+h2c 进行反向代理，对 naiveproxy 进行正向代理。包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、vless+h2c+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

4、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

6、naiveproxy （tls由vless+tcp+tls提供及处理，不需配置。）

v2ray tcp 类应用直连。v2ray ws 类应用分流一次。naiveproxy 回落(分流)一次。v2ray h2 类应用回落一次，分流（反代）一次，共计两次。

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现 h2 回落就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持 h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口或一个进程（Unix Domain Socket 应用）。

3、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray 的 h2（http/2）反向代理。

4、使用本人 github 中编译好的 caddy2 文件，才可同时支持 naiveproxy、h2 回落、h2（http/2）反向代理及 PROXY protocol 应用。

5、配置1：caddy2 没有启用 PROXY protocol（接收），仅端口回落。配置2：caddy2 没有启用 PROXY protocol（接收），仅进程回落。配置3：caddy2 启用了 PROXY protocol（接收），且进程回落。
