注意：

1、除 v2ray kcp 外,所用应用共用443端口。此端口由 caddy2 监听（即caddy2前置），反向代理分流 ws 与 h2。无 vless tcp 应用。

2、v2ray ws 类应用分流（反代）一次。v2ray h2 类应用分流（反代）一次。

3、caddy2 等于或大于 v2.2.0-rc.1 版才支持反向代理 v2ray h2(http/2) 应用。
