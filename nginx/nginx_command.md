> 查找nginx 配置 ：
```
find / |grep nginx.conf
```
> 查看log日志文件
```
tail -f xx.log
```
> 查看 nginx 位置
```
which nginx
```
> 查看 nginx 是否运行
```
ps aux|grep nginx
```
修改文件中的所有：
```
sed -i 's/\r$//' yourfile
```
环境变量
```
source /etc/profile
```
## 防火墙
查看防火墙状态
```
firewall-cmd --state
```
开启防火墙
```
systemctl start firewalld.service
```
开启端口
```
firewall-cmd --zone=public --add-port=443/tcp --permanent
–zone=public表示作用域为公共的
–add-port=443/tcp添加tcp协议的端口端口号为443
–permanent永久生效，如果没有此参数，则只能维持当前 服 务生命周期内，重新启动后失效；
```
关闭端口
```
firewall-cmd --zone=public --remove-port=8080/tcp --permanent
```
重启防火墙
```
systemctl restart firewalld.service
```
重新载入防火墙
```
firewall-cmd --reload
```
查看已开启的端口
```
firewall-cmd --list-ports
```