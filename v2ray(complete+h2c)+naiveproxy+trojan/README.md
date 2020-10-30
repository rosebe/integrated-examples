介绍：

此配置包括 v2ray、naiveproxy(caddy2) 及 trojan(trojan-go) 集成。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vless+h2c+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

注意：

1、利用 vless tcp 强大的回落/分流特性，实现了vless tcp 与任意 ws（WebSocket） 类应用完美共存；且vless tcp 以 http/1.1 或 http/2 自适应代理科学上网。

2、naiveproxy(caddy2) 使用本 github 文件，可同时支持 naiveproxy 及 v2ray h2（http/2）反向代理。

3、caddy2 同时为 v2ray 与 trojan 提供 web 回落服务。

4、因 trojan(trojan-go) 不支持 PROXY protocol，故统一不启用此项应用。

5、配置1：v2ray、naiveproxy(caddy2)、trojan(trojan-go) 各自公开一个监听端口，各自分别或配合提供服务。配置2：v2ray 通过配置相关参数为 v2ray、naiveproxy(caddy2)、trojan(trojan-go) 进行 SNI 分流（四层转发），实现共用443端口。
