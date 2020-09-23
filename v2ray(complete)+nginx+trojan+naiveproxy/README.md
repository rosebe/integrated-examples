注：

1、nginx为v2ray、trojan(trojan-go)、naiveproxy(caddy2)进行sni分流（四层转发），实现共用443端口。同时兼顾为v2ray与trojan(trojan-go)提供回落web服务应用。

2、v2ray tcp类应用直连，v2ray ws类应用分流一次。

3、naiveproxy直连。v2ray h2类应用分流（反代）一次。

3、trojan(trojan-go)直连。

4、naiveproxy(caddy2) 使用本github文件，才可以同时支持naiveproxy及v2ray h2反向代理。
