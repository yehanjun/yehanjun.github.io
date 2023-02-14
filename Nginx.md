Nginx
NGINX,改变配置想让它生效而不停止服务,如下两种方式都可以:
1.nginx -t; nginx -s reload 
2.nginx -t; kill -HUP
nginx -t 检查nginx配置的语法,操作前都要检查一下,很重要,发现错误可及时修正.
nginx 版本1.4.7
nginx
在修改了配置文件后，可以实现平滑重新加载配置文件，所有的work processes 重新启动，master不重启。若work process
被连接占用，会等待连接结束后再重启该进程。 在生产中很实用。
默认情况下操作：
nginx - t;  
nginx -s reload
当配置文件不在默认路径下的时候：
nginx -c
 path/conf   -t  ;     nginx -c  path/conf
 -s reload
经测试 -c 可以和 -s
参数同时使用

Nginx 启动报 [emerg] bind() to
0.0.0.0:XXXX failed (13: Permission denied)错误处理
 系统启动Nginx后，报 [emerg] bind() to 0.0.0.0:XXXX failed (13:
Permission denied)错误的处理方式，分为两种： 
第一种：端口小于1024的情况： 
[emerg] bind() to 0.0.0.0:80 failed (13: Permission denied) 
  原因是1024以下端口启动时需要root权限，所以sudo nginx即可.。
 
第二种：端口大于1024的情况： 
[emerg] bind() to
0.0.0.0:8380 failed (13: Permission denied) 
这种情况，需要如下操作： 
首先，查看http允许访问的端口： 
    semanage port -l | grep http_port_t
    http_port_t                    tcp      80, 81, 443, 488, 8008, 8009, 8443, 9000 
其次，将要启动的端口加入到如上端口列表中 
semanage port -a -t
http_port_t  -p tcp 8090 
如此即可解决如上问题。

