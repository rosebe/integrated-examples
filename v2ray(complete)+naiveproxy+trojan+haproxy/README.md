注：

1、vless tcp 以http/1.1或http/2自适应代理科学上网。

2、利用 vless tcp 强大的回落/分流特性，实现了vless tcp与任意 ws 类应用完美共存。

3、naiveproxy(caddy2)兼顾为v2ray与trojan(trojan-go)提供回落web服务应用。

4、naiveproxy(caddy2) 使用本github文件，才可以同时支持naiveproxy及v2ray h2反向代理。

5、haproxy或nginx为v2ray、naiveproxy(caddy2)、trojan(trojan-go)进行sni分流（四层转发），实现共用443端口。
