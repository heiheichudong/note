# docker 
> [我所看的教程视频](https://www.bilibili.com/video/BV1gr4y1U7CY?p=16&spm_id_from=pageDriver&vd_source=5f9dd98cc38ec92331fce4fe26d34760)
## 安装 docker Engine
> [文档链接](https://docs.docker.com/)   
> 点击 manuals标签（手册标签）  
> 选择docker engine --> 选择相应的系统
> 下载慢可以设置阿里的镜像
## 命令  
- ### 帮助类命令  
```
 启动 systemctl start docker  
 停止 systemctl stop docker  
 重启 systemctl restart docker  
 查看状态 systemctl status docker  
 开机启动 systemctl enable docker  
 查看概要信息 docker info  
 查看帮助 docker --help
 查看具体命令帮助 docker 具体命令 --help   如 docker cp --help
```
  
- ### 镜像命令
列出主机上的镜像
```
docker images -aq
 -a 列出所有  
 -q 只显示镜像ID  
```

搜索镜像:
```
docker search 镜像名称 
 
列出五个镜像名为xxx的镜像: 
docker search --limit 5 xxx  
 ```
下载镜像
```
docker pull 镜像名称:version  
docker pull redis:6.0.0
```
查看空间
```
docker system df 
```
删除镜像
```
删除镜像 参数-f强制删除 
docker rmi -f 镜像名:version   
 
删除多个 参数-f强制删除 
1) docker rmi -f 镜像名:version 镜像名:version 镜像名:version  
2) docker rmi -f $(docker images -aq)
```
### 容器命令
启动容器
```
docker run [OPTIONS] IMAGE [COMMAND] [ARG...]
OPTIONS:
--name="新名字"
-d 守护式容器（后台运行）
-i 以交互模式运行容器，通常与-t同时使用
-t 为容器重新分配一个伪输入终端，通常与-i同时使用

-P 随机端口映射（大写P）
-p 指定端口映射（小写p）

例：docker run -it ubuntu /bin/bash
```
退出容器
```
exit 退出时会关闭容器
ctrl+p+q 退出时不会关闭容器
docker exec -it 容器ID bashShell
```
重新进入容器
```
docker exec -it 容器ID bashShell （用exit退出时不会关闭容器）
docker attach 容器ID （用exit退出时会关闭容器）
```
列出正在运行的容器
```
docker ps
-a 列出所有（正在运行+历史运行）
-l 显示最近创建的容器
-n 显示最近n个创建容器
-q 静默模式，只显示容器编号
```
启动、重启、停止、强停容器
```
docker start 容器ID或容器名
docker restart 容器ID或容器名
docker stop 容器ID或容器名
docker kill 容器ID或容器名
```
删除容器
```
删除已停止的容器
docker rm 容器ID
一次性删除多个容器
docker rm -f $(docker ps -a -q)
docker ps -a -q|xargs docker rm
```
日志
```
docker log 容器ID
```
查看容器内运行的进程
```
docker top 容器ID
```
查看容器内部细节
```
docker inspect 容器ID
```
导出与导入
```
导出容器中的文件
docker cp 容器ID：路径 容器目标路径
导出镜像
docker export 容器ID > xxx.tar
恢复镜像
cat xxx.tar | docker import - xxx镜像用户/xxx镜像名:version
```
组装本地镜像提交
```
docker commit -m "提交信息" -a="作者" 容器ID 要创建的目标镜像名:version
```
虚悬镜像
```
查找虚悬镜像
docker images ls -f dangling=true
删除虚悬镜像
docker image prune
```

数据卷共享
```
docker run -it --privileged=true -v /宿主机绝对路径:/容器内绝对路径:rw 镜像名
-v (volumes-form)
--privileged 类似申请root权限
:rw 容器可读可写
:ro 容器只读
```
docker 网络
```
docker network ls 
```
容器随docker启动
```
启动时添加
docker run -d --restart=always tomcat
启动后忘了添加可以补上
docker container update --restart=always 容器名字
```
