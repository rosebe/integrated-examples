此集成配置中nginx同时为v2ray与trojan提供web回落服务,因trojan不支持PROXY protocol，故关闭此项服务。

此配置实现 vless tcp 以http/1.1或http/2自适应代理科学上网，分流出ws，非v2ray的web回落给nginx。

注：

1、配置1：v2ray与trojan各自公开一个监听端口，各自分别提供科学上网服务。

2、配置2：nginx为v2ray、trojan(trojan-go)进行sni分流（四层转发），实现共用443端口。

