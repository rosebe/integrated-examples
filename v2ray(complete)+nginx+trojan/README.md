介绍：

此配置包括 v2ray 与 trojan（trojan-go）集成。nginx 同时为 vless+tcp 与 trojan（trojan-go）提供 web 回落服务。v2ray 包括如下应用：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）


注意：

1、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程，故回落端口或进程必须分开。

2、nginx 不支持 h2c proxy，故 nginx 不能实现 v2ray 的 h2（http/2）反向代理。

3、nginx 预编译程序包一般不带支持 SNI 分流协议的模块。如要使用此项协议应用，需加 stream_ssl_preread_module 模块构建自定义模板，再进行源代码编译和安装。

4、因 v2ray SNI 分流不支持 PROXY protocol（发送），故配置2不启用此项应用。

5、因 trojan(trojan-go) 不支持 PROXY protocol（接收），而 nginx SNI 中的 PROXY protocol 发送是针对共用端口全局模式，故配置3不启用此项应用。

6、配置1：v2ray 与 trojan 各自公开一个对外端口，分别提供科学上网服务。配置2：v2ray 通过配置相关参数为 v2ray、trojan(trojan-go) 进行 SNI 分流（四层转发），除 v2ray kcp 外，实现共用443端口。配置3：nginx 为 v2ray、trojan(trojan-go) 进行 SNI 分流（四层转发），除 v2ray kcp 外、实现共用443端口。
