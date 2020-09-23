除v2ray kcp外,所用应用共用443端口。此端口由v2ray监听（即v2ray前置），利用vless tcp回落/分流特性实现，分流出ws，非v2ray的web回落给nginx，无vless h2应用。

注意：

1、nginx 支持 h2c server，但不支持http/1.1 server与h2c server共用一个端口或一个进程。

2、v2ray tcp类应用直连，且以http/1.1或http/2自适应代理科学上网；v2ray ws类应用分流一次。
