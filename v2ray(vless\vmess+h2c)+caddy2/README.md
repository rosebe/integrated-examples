介绍：

通过 caddy2 前置 v2ray server 实现 h2（h2c+tls） 反向代理，tls 由 caddy2 提供及处理。

原理图： v2ray client <------ h2 ------> caddy2 <- h2c -> v2ray server

注意： 

1、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray 的 h2（http/2）反向代理。

2、nginx 不支持 h2c proxy，故不能用 nginx 来实现 v2ray 的 h2（http/2）反向代理。
