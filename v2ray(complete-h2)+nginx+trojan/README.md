注：

1、nginx同时为v2ray与trojan提供web回落服务。

2、nginx 支持 h2c server，但不支持http/1.1 server与h2c server共用一个端口或一个进程，故回落端口或进程必须分开。

4、nginx 不支持 h2c proxy，故无法搭建vless\vmess+h2反代应用。

5、因trojan不支持PROXY protocol，故统一不启用此项应用。

6、实现 vless tcp 以http/1.1或http/2自适应代理科学上网，分流出ws，非v2ray的web回落给nginx。

7、配置1：v2ray与trojan各自公开一个监听端口，各自分别提供科学上网服务。

8、配置2：nginx为v2ray、trojan(trojan-go)进行sni分流（四层转发），除v2ray kcp外,实现共用443端口。

