介绍：

此配置包括 v2ray、trojan(trojan-go) 及 naiveproxy(caddy2) 应用。nginx 同时为 vless+tcp 与 trojan(trojan-go) 提供 web 回落服务。caddy2 同时为 vless/vmess+h2c 提供反向代理，为 naiveproxy 提供正向代理。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、vless+h2c+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

4、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

注意：

1、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程，故回落端口或进程必须分开。

2、nginx 预编译程序包不带支持 SNI 分流协议的模块。如要使用此项协议应用，需加 stream_ssl_preread_module 模块构建自定义模板，再进行源代码编译和安装。

3、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray 的 h2（http/2）反向代理。

4、使用本人 github 中编译好的 caddy2 文件，才可同时支持 naiveproxy、h2（http/2）反向代理的应用。

5、因 v2ray SNI 分流不支持 PROXY protocol（发送），故配置2不启用此项应用。

6、因 trojan(trojan-go) 不支持 PROXY protocol（接收），而 nginx SNI 中的 PROXY protocol 发送是针对共用端口全局模式，故配置3不启用此项应用。

7、因 trojan(trojan-go) 不支持 Unix Domain Socket，故所有配置没有采用进程回落。

8、配置1：v2ray、trojan(trojan-go)、naiveproxy(caddy2) 各自公开一个监听端口，各自分别或配合提供服务。配置2：v2ray 通过配置相关参数为 v2ray、trojan(trojan-go)、naiveproxy(caddy2) 进行 SNI 分流（四层转发），除 v2ray kcp 外、实现共用443端口。配置3：nginx 为 v2ray、trojan(trojan-go)、naiveproxy(caddy2) 进行 SNI 分流（四层转发），除 v2ray kcp 外、实现共用443端口。

