介绍：

通过caddy2前置v2ray server实现 h2 反向代理。

原理图： v2ray client <----- h2 ------> caddy2 <- h2c -> v2ray server

注意： 

1、caddy2 等于或大于 v2.2.0-rc.1 版才支持反向代理 v2ray H2(HTTP/2) 应用，即 caddy2 支持 h2c proxy。

2、nginx 不支持 h2c proxy，故 nginx 不能实现 v2ray h2 反向代理。
