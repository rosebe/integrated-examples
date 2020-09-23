注：

1、nginx为v2ray与trojan(trojan-go)提供回落服务。

2、nginx 支持 h2c server，但不支持http/1.1 server与h2c server共用一个端口或一个进程，故回落端口或进程必须分开。

3、nginx 不支持 h2c proxy，故无法搭建vless\vmess+h2反代应用。

4、因trojan不支持PROXY protocol，故统一不启用此项应用。

5、v2ray vless+tcp 以http/1.1或http/2自适应代理科学上网。

6、利用 vless tcp 强大的回落/分流特性，实现了vless tcp与任意 ws 类应用完美共存。

7、naiveproxy(caddy2) 使用本github文件，才可以同时支持naiveproxy及v2ray h2反向代理。

8、配置1：v2ray、naiveproxy(caddy2)、trojan(trojan-go)各自公开一个监听端口，各自分别或配合提供服务。

9、配置2：nginx为v2ray、trojan(trojan-go)、naiveproxy(caddy2)进行sni分流（四层转发），实现共用443端口。

