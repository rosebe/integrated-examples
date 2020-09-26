注意：

1、vless tcp 以http/1.1或http/2自适应代理科学上网。

2、利用 vless tcp 强大的回落/分流特性，实现了vless tcp与任意 ws 类应用完美共存。

3、naiveproxy(caddy2) 使用本github文件，才可以同时支持naiveproxy及v2ray h2反向代理。

4、nginx同时为v2ray与trojan提供web回落服务。

5、因trojan与naiveproxy都不支持PROXY protocol，故统一不启用此项应用。

6、nginx 支持 h2c server，但不支持http/1.1 server与h2c server共用一个端口或一个进程，故回落端口或进程必须分开。

7、nginx 不支持 h2c proxy，故无法搭建vless\vmess+h2反代应用。

8、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加stream_ssl_preread_module模块构建自定义模板，再进行源代码编译和安装。

9、配置1：v2ray、trojan(trojan-go、naiveproxy(caddy2))各自公开一个监听端口，各自分别或配合提供服务。

10、配置2：nginx为v2ray、trojan(trojan-go)、naiveproxy(caddy2)进行SNI分流（四层转发），实现共用443端口。

