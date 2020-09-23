注：

1、naiveproxy(caddy2)兼顾为v2ray与trojan(trojan-go)提供回落web服务应用。

2、nginx为v2ray、naiveproxy(caddy2)、trojan(trojan-go)进行sni分流（四层转发），实现共用443端口。

3、v2ray tcp类应用直连，v2ray ws类应用分流一次。

4、naiveproxy(caddy2) 直连。v2ray h2类应用分流（反代）一次。

5、trojan(trojan-go)直连。

6、naiveproxy(caddy2) 使用本github文件，才可以同时支持naiveproxy及v2ray h2反向代理。
