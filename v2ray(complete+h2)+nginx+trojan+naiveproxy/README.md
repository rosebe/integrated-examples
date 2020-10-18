介绍：

此配置包括v2ray、trojan(trojan-go)及naiveproxy(caddy2)应用。nginx同时为v2ray与trojan(trojan-go)提供回落服务。v2ray包括如下应用：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls处理，不需要配置；另可改成vmess+ws+tls。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls处理，不需要另外配置。）

4、vless+h2 （tls由caddy2处理，不需要另外配置；另可改成vmess+h2。）

5、vmess+kcp+seed（可改成vless+kcp+seed。）

注意：

1、利用 vless tcp 强大的回落/分流特性，实现了vless tcp与任意 ws 类应用完美共存；且vless tcp 以http/1.1或http/2自适应代理科学上网。

2、naiveproxy(caddy2) 使用本github文件，可同时支持naiveproxy及v2ray h2反向代理。

3、nginx同时为v2ray与trojan提供web回落服务。

4、因trojan(trojan-go)不支持PROXY protocol，故统一不启用此项应用。

5、nginx 支持 h2c server，但不支持http/1.1 server与h2c server共用一个端口或一个进程，故回落端口或进程必须分开。

6、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加stream_ssl_preread_module模块构建自定义模板，再进行源代码编译和安装。

7、配置1：v2ray、trojan(trojan-go、naiveproxy(caddy2))各自公开一个监听端口，各自分别或配合提供服务。配置2：nginx为v2ray、trojan(trojan-go)、naiveproxy(caddy2)进行SNI分流（四层转发），实现共用443端口。

