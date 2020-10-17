注意：

1、vless tcp 以http/1.1或http/2自适应代理科学上网。

2、利用 vless tcp 强大的回落/分流特性，实现了vless tcp与任意 ws 类应用完美共存。

3、naiveproxy(caddy2)兼顾为v2ray与trojan(trojan-go)提供回落web服务应用。

4、naiveproxy（caddy2）使用本人github文件，可同时支持naiveproxy、回落 h2 及v2ray h2反向代理。

5、用haproxy或nginx为v2ray、naiveproxy(caddy2)、trojan(trojan-go)进行SNI分流（四层转发），实现共用443端口。

6、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加stream_ssl_preread_module模块构建自定义模板，再进行源代码编译和安装。另nginx SNI分流是全局模式，不支持域名（内部端口）分流。

7、caddy2 发行版不支持 PROXY protocol，如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译或选使用本人github文件即可。

8、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
