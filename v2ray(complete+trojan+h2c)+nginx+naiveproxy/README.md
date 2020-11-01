一、回落终极部署（套娃方式）

v2ray、naiveproxy(caddy2) 各自公开一个监听端口，各自分别或配合提供服务。配置1/配置2/配置3实现了 vless+tcpp 以 http/1.1 代理科学上网，分流出 ws（WebSocket） 应用，回落给 trojan+tcp，trojan+tcp 处理后再回落给 nginx。另 caddy2 还同时为 vless/vmess+h2c 提供反向代理，为 naiveproxy 提供正向代理。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vless+h2c+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

6、trojan+tcp+tls（tls由vless+tcp+tls提供及处理，不需配置。）

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan+tcp 及完整回落。

2、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程；而v2ray 的 trojan+tcp 不支持端口或进程分离 h2 回落，故套娃回落 nginx 只能全部采用 h1 回落；因vless+tcp 与 trojan+tcp 无 h2 连接，可能影响速度。

3、nginx 预编译程序包可能不带支持 PROXY protocol 协议的模块。如要使用此项协议应用，需加 http_realip_module（必须加） 及 stream_realip_module（可选加） 两模块构建自定义模板，再进行源代码编译和安装。另编译时选取源代码版本建议不要低于1.13.11。

4、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray 的 h2（http/2）反向代理。

5、使用本人 github 中编译好的 caddy2 文件，才可同时支持 naiveproxy、h2（http/2）反向代理的应用。

6、配置1：没有启用 PROXY protocol，仅端口回落。配置2：启用了 PROXY protocol，且端口回落。配置3：启用了 PROXY protocol，且进程回落。

二、v2ray SNI分流优化共用443端口

v2ray 通过配置相关参数对 vless+tcp、trojan+tcp、naiveproxy(caddy2) 进行端口分流（四层转发），实现共用443端口。配置4实现了 vless+tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出 ws（WebSocket） ，回落给 nginx。同时 trojan+tcp 也以 http/1.1 代理科学上网，回落给 nginx。另 caddy2 还同时为 vless/vmess+h2c 提供反向代理，为 naiveproxy 提供正向代理。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vless+h2c+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

6、trojan+tcp+tls（回落配置。）

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan+tcp 及完整回落。

2、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程。v2ray 的 trojan+tcp 不支持端口或进程分离 h2 回落，故只能采用 h1 回落；因 trojan+tcp 无 h2 连接，可能影响速度。

3、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray 的 h2（http/2）反向代理。

4、使用本人 github 中编译好的 caddy2 文件，才可同时支持 naiveproxy、h2（http/2）反向代理的应用。

5、v2ray SNI分流不支持 PROXY protocol ，故配置4：没有启用 PROXY protocol，仅端口回落。

三、nginx SNI分流优化共用443端口

利用 nginx 支持 SNI 分流特性，对 vless+tcp、trojan+tcp、naiveproxy(caddy2) 进行端口分流（四层转发），实现共用443端口。配置5/配置6/配置7实现了 vless+tcp 以 http/1.1 或 http/2 自适应代理科学上网，分流出 ws（WebSocket） ，回落给 nginx。同时 trojan+tcp 也以 http/1.1 代理科学上网，回落给 nginx。另 caddy2 还同时为 vless/vmess+h2c 提供反向代理，为 naiveproxy 提供正向代理。v2ray 包括应用如下：

1、vless+tcp+tls（回落/分流配置。）

2、vless+ws+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vmess+ws+tls、SS+v2ray-plugin+tls、trojan+ws+tls应用。）

3、SS+v2ray-plugin+tls（tls由vless+tcp+tls提供及处理，不需配置；另可改成或添加vless+ws+tls、vmess+ws+tls、trojan+ws+tls应用。）

4、vless+h2c+tls（tls由caddy2提供及处理，不需配置；另可改成或添加vmess+h2c+tls应用。）

5、vmess+kcp+seed（可改成vless+kcp+seed，或添加它。）

6、trojan+tcp+tls（回落配置。）

注意：

1、v2ray v4.31.0 版本及以后才支持 trojan+tcp 及完整回落。

2、nginx 支持 h2c server，但不支持 http/1.1 server 与 h2c server 共用一个端口或一个进程。v2ray 的 trojan+tcp 不支持端口或进程分离 h2 回落，故只能采用 h1 回落；因 trojan+tcp 无 h2 连接，可能影响速度。

3、nginx 预编译程序包可能不带支持 PROXY protocol 协议的模块。如要使用此项协议应用，需加 http_realip_module 及 stream_realip_module 两模块构建自定义模板，再进行源代码编译和安装。另编译时选取源代码版本建议不要低于1.13.11。

4、nginx 预编译程序包不带支持SNI分流协议的模块。如要使用此项协议应用，需加 stream_ssl_preread_module 模块构建自定义模板，再进行源代码编译和安装。

5、caddy2 等于或大于 v2.2.0-rc.1 版才支持 h2c proxy，即支持 v2ray 的 h2（http/2）反向代理。

6、使用本人 github 中编译好的 caddy2 文件，才可同时支持 naiveproxy、h2（http/2）反向代理的应用。

7、配置5：没有启用 PROXY protocol，仅端口回落。配置6：启用了 PROXY protocol，且端口回落。配置7：启用了 PROXY protocol，且进程回落。
