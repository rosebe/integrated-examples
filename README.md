**这里是主流科学上网的优化配置及最优组合示例。如是不太了解科学上网，建议先依次从简单到复杂参考及部署。**

### 单一应用服务器端配置示例
1. [v2ray(vless\vmess+kcp+seed)](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%5Cvmess%2Bkcp%2Bseed)) （若网络极差，推荐部署。）  
2. [v2ray(vless\vmess+ws)+caddy2\nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%5Cvmess%2Bws)%2Bcaddy2%5Cnginx) （WebSocket的caddy2或nginx反向代理，之前推荐部署。）  
3. [v2ray(vless\vmess+h2c)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%5Cvmess%2Bh2c)%2Bcaddy2) （http/2的caddy2反向代理。）  
4. [v2ray(SS+v2ray-plugin)+caddy2\nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(SS%2Bv2ray-plugin)%2Bcaddy2%5Cnginx) （兼容shadowsocks的WebSocket应用，caddy2或nginx反向代理。）  
5. [v2ray(vless+tcp+tls)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%2Btcp%2Btls)%2Bcaddy2) （以h2或http/1.1任意连接实现正向代理，web回落给caddy2。）  
6. [v2ray(vless+tcp+tls)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%2Btcp%2Btls)%2Bnginx) （以h2或http/1.1任意连接实现正向代理，web回落给nginx。）  
7. [v2ray(trojan+tcp+tls)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(trojan%2Btcp%2Btls)%2Bcaddy2) （兼容trojan应用，以h2或http/1.1任意连接实现正向代理，web回落给caddy2。）  
8. [v2ray(trojan+tcp+tls)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(trojan%2Btcp%2Btls)%2Bnginx) （兼容trojan应用，以h2或http/1.1连接实现正向代理，web回落给nginx。）  
9. [v2ray(trojan+ws)+caddy2\nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(trojan%2Bws)%2Bcaddy2%5Cnginx) （兼容trojan-go的WebSocket应用，caddy2或nginx反向代理。）  
---
1. [trojan\trojan-go+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/trojan%5Ctrojan-go%2Bcaddy2) （trojan或trojan-go应用，以h2或http/1.1任意连接实现正向代理，web回落给caddy2。）  
2. [trojan\trojan-go+nginx](https://github.com/lxhao61/integrated-examples/tree/master/trojan%5Ctrojan-go%2Bnginx) （trojan或trojan-go应用，以h2或http/1.1连接实现正向代理，web回落给nginx。）  
---
1. [naiveproxy(caddy2+forwardproxy)](https://github.com/lxhao61/integrated-examples/tree/master/naiveproxy(caddy2%2Bforwardproxy)) （naiveproxy应用，以http/2或http/3正向代理。）  

### 综合应用服务器端配置示例
#### 1. v2ray或Xray为主、caddy2为辅及其它应用。
1. [v2ray(complete+h2c-tcp)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c-tcp)%2Bcaddy2) （caddy2前置，反向代理WebSocket与http/2的综合应用；之前推荐部署。）  
2. [v2ray(complete+h2c-tcp)+naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c-tcp)%2Bnaiveproxy) （上一项应用+naiveproxy应用。）  
---
1. [v2ray(vless+tcp&ws+tls)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%2Btcp%26ws%2Btls)%2Bcaddy2) （推荐部署，同时支持vless+tcp与WebSocket类应用，web回落给caddy2。）  
2. [v2ray(vless+tcp&ws+tls)+naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%2Btcp%26ws%2Btls)%2Bnaiveproxy) （上一项应用+naiveproxy应用。）  
3. [v2ray(complete+h2c)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c)%2Bcaddy2) （v2ray或Xray综合应用+反向代理http/2应用。）  
4. [v2ray(complete+h2c)+naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c)%2Bnaiveproxy) （上一项应用+naiveproxy应用。）  
5. [v2ray(complete+h2c)+naiveproxy+trojan](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c)%2Bnaiveproxy%2Btrojan) （上一项应用+trojan应用及共用端口。）  
6. [v2ray(complete+h2c)+naiveproxy+trojan+haproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c)%2Bnaiveproxy%2Btrojan%2Bhaproxy) （用haproxy对上一项应用进行SNI分流，共用端口。）  
---
1. [v2ray(vless&trojan+tcp&ws+tls)+caddy2](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%26trojan%2Btcp%26ws%2Btls)%2Bcaddy2) （回落终极部署/套娃方式，或共用端口。）  
2. [v2ray(complete+trojan+h2c)+naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Btrojan%2Bh2c)%2Bnaiveproxy) （v2ray或Xray全部应用+naiveproxy应用及共用端口。）  
3. [v2ray(complete+trojan+h2c)+naiveproxy+haproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Btrojan%2Bh2c)%2Bnaiveproxy%2Bhaproxy) （用haproxy对上一项应用进行SNI分流，共用端口。）  
#### 2. v2ray或Xray为主、nginx为辅及其它应用。  
1. [v2ray(complete-tcp)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete-tcp)%2Bnginx) （nginx前置，反向代理WebSocket的综合应用；之前推荐部署。）  
---
1. [v2ray(vless+tcp&ws+tls)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%2Btcp%26ws%2Btls)%2Bnginx) （推荐部署，同时支持vless+tcp与WebSocket类应用，web回落给nginx。）  
2. [v2ray(complete)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete)%2Bnginx) （v2ray或Xray综合应用。）  
3. [v2ray(complete)+nginx+trojan](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete)%2Bnginx%2Btrojan) （上一项应用+trojan应用及共用端口。）  
4. [v2ray(complete+h2c)+nginx+trojan+naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Bh2c)%2Bnginx%2Btrojan%2Bnaiveproxy) （上一项应用+naiveproxy+反向代理http/2应用及共用端口。）  
---
1. [v2ray(vless&trojan+tcp&ws+tls)+nginx](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(vless%26trojan%2Btcp%26ws%2Btls)%2Bnginx) （回落终极部署/套娃方式，或共用端口。）  
2. [v2ray(complete+trojan+h2c)+nginx+naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(complete%2Btrojan%2Bh2c)%2Bnginx%2Bnaiveproxy) （v2ray或Xray全部应用+naiveproxy应用及共用端口。）  
#### 3. trojan或trojan-go为主、naiveproxy为辅应用。
1. [trojan\trojan-go+naiveproxy](https://github.com/lxhao61/integrated-examples/tree/master/trojan%5Ctrojan-go%2Bnaiveproxy) （trojan或trojan-go应用+naiveproxy应用。）  
---
**以上所有实例（含单一与综合示例）注意:** 
1. 所有v2ray或Xray配置文件都配置了禁用BT。如不需要，可以删除相关配置（参考v2ray(other configuration)中BT_config.json文件）。  
2. v2ray从版本v4.33.0删除了xtls应用，故若还想用xtls应用，请选Xray。Xray是v2ray分支，也是因为这个应用分家。另外注意：配置示例中log部分的路径名称，需修改为对应的xray或v2ray。   
3. 除v2ray(vless\vmess+kcp+seed)示例外，回落或反代网站都支持http自动跳转到https。  
4. complete表示包含v2ray或Xray的vless+tcp+tls、vless+ws+tls、SS+v2ray-plugin+tls、vmess+kcp+seed的综合应用。  
5. naiveproxy=caddy2+forwardproxy。此程序文件已编译好，本人github下载即可。  **

### 特殊应用服务器端配置示例
1. [v2ray(other configuration)](https://github.com/lxhao61/integrated-examples/tree/master/v2ray(other%20configuration)) （v2ray或Xray其它多种特殊应用配置方法。）  
2. [caddy2(other configuration)](https://github.com/lxhao61/integrated-examples/tree/master/caddy2(other%20configuration)) （分别回落caddy2不同网站的配置方法。）  
3. [nginx(other configuration)](https://github.com/lxhao61/integrated-examples/tree/master/nginx(other%20configuration)) （nginx SNI分流v2ray或Xray回落应用与网站应用的配置方法。） 

### client configuration  
    [官方客户端文本配置示例](https://github.com/lxhao61/integrated-examples/tree/master/client%20configuration)（使用图形界面客户端仅参考即可）

### service configuration  
   [程序service配置示例](https://github.com/lxhao61/integrated-examples/tree/master/service%20configuration)（手工配置程序由操作系统管理及自动运行可参考）

### 使用/贡献指南  
1. 若程序增加新功能，开始在单一应用服务器端配置示例中添加；过一段时间稳定后才会综合应用服务器端配置示例中添加。如除trojan+tcp套娃外，vless+tcp及trojan+tcp的xtls已全部加上。  
2. 欢迎你提交 PR ,如对现行配置示例优化修订，或将自己使用的配置制作模板提交等。
