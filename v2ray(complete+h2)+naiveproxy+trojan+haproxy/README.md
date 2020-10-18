介绍：

此配置包括v2ray、naiveproxy(caddy2)及trojan(trojan-go)应用。用haproxy或nginx为v2ray、naiveproxy(caddy2)、trojan(trojan-go)进行SNI分流（四层转发），实现共用443端口。另caddy2还同时为v2ray与trojan(trojan-go)提供回落服务。v2ray包括如下应用：

1、vless+tcp+tls

2、vless+ws+tls（tls由vless+tcp+tls处理，不需要配置；另可改成vmess+ws+tls。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls处理，不需要另外配置。）

4、vless+h2 （tls由caddy2处理，不需要另外配置；另可改成vmess+h2。）

5、vmess+kcp+seed（可改成vless+kcp+seed。）

注意：

1、利用 vless tcp 强大的回落/分流特性，实现了vless tcp与任意 ws 类应用完美共存；且vless tcp 以http/1.1或http/2自适应代理科学上网。

2、naiveproxy（caddy2）使用本人github文件，可同时支持naiveproxy、回落 h2 及v2ray h2反向代理。

3、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加stream_ssl_preread_module模块构建自定义模板，再进行源代码编译和安装。

4、nginx 支持 PROXY protocol 协议。但是针对共用端口是全局模式，不支持区分域名（或内部端口）发送。而trojan(trojan-go)不支持PROXY protocol，故不能用nginx SNI分流，且开启PROXY protocol发送。

5、caddy2 发行版不支持 PROXY protocol，如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译或选使用本人github文件即可。

6、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。
