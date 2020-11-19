nginx SNI 分流 v2ray 与网站配置方法

此方法解决 v2ray 回落应用与网站应用（原网站不想做回落网站，或 nginx/caddy2 等有多个网站应用。）共存问题。此配置示例参考对应‘nginx SNI 分流优化共用443端口’中的 nginx 配置示例。

注意：

1、nginx 预编译程序包一般不带支持 SNI 分流协议的模块。如要使用此项协议应用，需加 stream_ssl_preread_module 模块构建自定义模板，再进行源代码编译和安装。

2、若系统版本过低，其对应发行版仓库自带 nginx 预编译程序包可能不支持 tls1.3；如需要支持 tls1.3，必须先升级 OpenSSl 版本大于 1.1.1，再进行 nginx 源代码编译和安装。

3、也可以用 haproxy SNI 分流 v2ray 回落应用与网站应用来解决共存问题。但若已采用 nginx 来做回落 web 服务器，不推荐（无必要再增加软件）；若采用非 nginx 来做回落 web 服务器，推荐采用 haproxy SNI 分流解决。
