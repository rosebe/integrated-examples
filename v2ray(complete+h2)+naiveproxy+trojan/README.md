注意：

1、v2ray、caddy2(naiveproxy)、trojan(trojan-go)各自公开一个监听端口，各自分别或配合提供服务。如caddy2还同时为v2ray与trojan(trojan-go)提供回落服务。

2、v2ray tcp类应用直连，v2ray ws类应用分流一次。

3、naiveproxy直连。v2ray h2类应用分流（反代）一次。

3、trojan(trojan-go)直连。

4、naiveproxy（caddy2）使用本人github文件，可同时支持naiveproxy、回落 h2 及v2ray h2反向代理。
