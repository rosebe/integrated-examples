注：

1、vless tcp 以http/1.1或http/2自适应代理科学上网。

2、利用 vless tcp 强大的回落/分流特性，实现了vless tcp与任意 ws 类应用完美共存。

3、naiveproxy(caddy2)兼顾为v2ray与trojan(trojan-go)提供回落web服务应用。

4、naiveproxy（caddy2）使用本人github文件，才可以同时支持naiveproxy、回落 h2 及v2ray h2反向代理。

5、haproxy或nginx为v2ray、naiveproxy(caddy2)、trojan(trojan-go)进行SNI分流（四层转发），实现共用443端口。

6、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加stream_ssl_preread_module模块构建自定义模板进行源代码编译和安装。
