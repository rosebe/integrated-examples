注：

1、naiveproxy(caddy2)兼顾为v2ray与trojan(trojan-go)提供回落web服务应用。

2、naiveproxy(caddy2) 使用本github文件，才可以同时支持naiveproxy及v2ray h2反向代理。

3、haproxy或nginx为v2ray、naiveproxy(caddy2)、trojan(trojan-go)进行sni分流（四层转发），实现共用443端口。
