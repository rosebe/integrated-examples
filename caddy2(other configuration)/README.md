回落caddy2多个网站的分流配置方法

此方法解决v2ray前置监听443后，不影响原来caddy2前置时，不同域名访问不同网站问题。

注意：也可以用 haproxy SNI 分流 v2ray 回落应用与网站（原网站不想做回落网站，或 caddy2 等有多个网站应用。）应用来解决问题（不同方法，达到相同效果。）。配置示例参考 ‘v2ray(complete+h2c)+naiveproxy+trojan+haproxy’或‘v2ray(complete+trojan+h2c)+naiveproxy+haproxy’中 haproxy SNI 分流示例。
