v2ray、caddy2(naiveproxy)各自公开一个监听端口，各自分别或配合提供服务。如caddy2还同时为v2ray与trojan(trojan-go)提供回落服务。

此配置实现 vless tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出ws，回落给 trojan，由 trojan 处理后再回落给 caddy2。（套娃方式）

利用 vless 强大的回落/分流特性，实现了共用 443 端口，同时支持 vless tcp 与任意 ws 类及trojan 应用完美共存。

v2ray tcp类应用直连，v2ray ws类应用分流一次。

naiveproxy直连。v2ray h2类应用分流（反代）一次。

注意：

1、caddy2 目前只能 json 配置才能开启 h2c server，故要实现回落 h2 就不能采用 Caddyfile 配置；另外caddy2 版本不能低于 v2.1.0 ，否则不支持h2c server。

2、caddy2 支持 http/1.1 server 与 h2c server 共用一个端口。

3、caddy2 发行版不支持 PROXY protocol，如要支持 PROXY protocol 需选 caddy2-proxyprotocol 插件定制编译或选使用本人github文件即可。

4、v2ray v4.31.0 版本及以后才支持 trojan 及完整回落。

5、全部配置没有启用 PROXY protocol，仅端口回落。因觉得caddy2已单独公开一个监听端口，对web服务来说已经足够。

6、用haproxy或nginx为v2ray、naiveproxy(caddy2)进行SNI分流（四层转发），实现共用443端口。

7、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加stream_ssl_preread_module模块构建自定义模板，再进行源代码编译和安装。
