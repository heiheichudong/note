   搭建Idea授权服务器用于学习 


[搭建Idea授权服务器用于学习](https://www.cnblogs.com/wenyule/p/ideaserver.html)
--------------------------------------------------------------------

我自己的搭建服务器http://doit.wenyule.top

懒得看教程或弄不好的小伙伴可以用我搭建的，在激活那选择服务器，输入我上面的地址，注意可以激活2018.2.1之前的。为了防止用的人太多被封，你也可以搭建自己的服务器。或者使用脚本。有能力的鼓励支持正版。有什么问题可以在下面留言。　　

     这里用到的脚本是大神写的，具体可以查看链接----》地址:[http://idea.lanyus.com/](http://idea.lanyus.com/) 刚开始，懒得折腾的小伙伴，可以直接去用大神的注册码先用着。

1.  想要长久，又不想麻烦的，可以去下载本地服务器【就是用于接收激活请求的】的exe程序运行后输入给出的ip地址即可（适合刚开始的小白，但也存在过一段时间会失效需要重新运行本地程序，再次输入运行给出本地ip和端口激活，没有强迫症的，将就用也挺好的）。下载的链接：[https://pan.baidu.com/s/1f9lrfcQ951aIrPZlbL4jVw](https://pan.baidu.com/s/1f9lrfcQ951aIrPZlbL4jVw%20) 提取码：hkdn
2.  如果不想隔断时间自己运行本地的程序去激活的话，有一个属于自己的很长久的服务器，那么下面的方法正是。

在搭建idea服务器之前确保你手里面拥有一台服务器，因为下面的操作不同于本地（你都知道本地只需要管理员身份运行本地服务器exe程序后，就可以在你的相应产品里面激活，然而这样有一个弊端就是过几天可能就要重新激活一便很麻烦），之所以要在服务器上，就是把每次你软件激活请求交给远端的服务器去做，而不是每次都去运行一遍本地激活程序。说白了就是把那个激活程序放到远端服务器上面，让他24小时运行，这样就可以免去很多麻烦。

         官方对授权服务器进行了更新，这里搭建的激活服务器只对2018-2-1之前的IDE管用，之后的就激活不了，追求更新的可以搜索看其他教程：添加hosts文件和脚本什么的，这里不做介绍。个人觉得没必要追求太新，够用就行。

云服务器介绍教程：-->[点击这me](https://www.cnblogs.com/wenyule/p/9233383.html)   或者搬瓦工也挺不错：--->[搬瓦工 ](https://bwh8.net/cart.php?aff=39094)

 本次实验环境
```
[root@bwg-cs6 ~]# uname -r
4.16.13-1.el6.elrepo.x86_64
[root@bwg-cs6 ~]# cat /etc/redhat-release 
CentOS release 6.9 (Final)
```
一.上传脚本运行文件
----------

文件下载，大佬的地址：http://blog.lanyus.com/archives/317.html

或者直接 下载下面实验需要的单个文件（linux\_64）链接: https://pan.baidu.com/s/1Yf6N1gDq\_-E3kcIl8moxvA 提取码: fvvi

上传到服务器，可使用lrzsz,SecureCRT自带有ftp功能，这里不再赘述。

使用rz 上传 提前安装lrzsz
```
yum -y install lrzsz
```
安装完成后，在终端输入rz，弹出上传窗口，上传文件即可

 注意：这里是在linux_64环境下搭建，解压后不要选错上传的文件。

二.安装idea破解服务之前准备
----------------
```
# 创建一个家目录存放，激活用的脚本
mkdir /home/IntellijIdea　　
mv IntelliJIDEALicenseServer_linux_amd64 /home/IntellijIdea/IdeaServer  
cd /home/IntellijIdea
chmod +x IdeaServer        #并添加上执行权限
```
三.添加后台运行方法
----------

添加到后台运行

方式1\[推荐\]：用screen在后台运行

　　优点是简单方便，但重启后需要再次重新添加，也可以添加到开机自启项目中。（这里主要是以这种方式实现的）
```
#安装screen
yum install screen -y  
# 启动程序
screen -dmS IdeaServer -d -m /home/IntellijIdea/IdeaServer -p 1029 -u Lewen -prolongationPeriod 999999999999
     [后台启动] [服务名]  　　　　[脚本位置]  　　　　　　　　　　　[运行的端口][用户名]

[注释]：关键参数替换成你自己的
screen -dmS     后台运行
IdeaServer        服务名称[你也可以叫别的]
d -m /home/IntellijIdea/IdeaServer      你脚本存放的路径
-p 1029             服务绑定的端口[不要与系统的端口冲突]
-u Lewen           用户名[自定义起]
-prolongationPeriod 999999999999     有限时间　　

```

方式2：以超级进程的方式添加，需要安装supervisor

　　过程比较繁琐，但后续启动重启服务比较方便。[可以自己尝试]
```
安装
easy_install supervisor
创建超级目录
mkdir /etc/supervisor/config.d -p

cd /etc/supervisor/
总的配置文件
echo_supervisord_conf > /etc/supervisor/supervisord.conf

该目录下放配置文件
cd config.d/ 

vi IdeaServer.conf
#按照格式，添加命令

[program:idea-server]

command=/home/IntellijIdea/IdeaServer -p 1027 -u Lewen -prolongationPeriod 999999999999
autostart=true
autorestart=true
startsecs=3    
    
    
supervisord -c /etc/supervisor/supervisord.conf
查看状态
supervisorctl status    
启动服务
supervisorctl start 服务名
```
备注：supervisorctl的用法
----------
```
supervisord : 启动supervisor
supervisorctl   reload          //修改完配置文件后重新启动supervisor
supervisorctl   status          //查看supervisor监管的进程状态
supervisorctl   start 进程名    //启动XXX进程
supervisorctl   stop 进程名     //停止XXX进程
supervisorctl   stop all         //停止全部进程，注：start、restart、stop都不会载入最新的配置文件。
supervisorctl update           //根据最新的配置文件，启动新配置或有改动的进程，配置没有改动的进程不会受影响而重启
```

运行起来后可以看到linux服务器本地对应的端口开启了

![](https://img2018.cnblogs.com/blog/1165731/201810/1165731-20181013085622177-905473468.png)

     这时候只是在Linux服务器本地开启了端口，说明激活服务已经起来了。但这时只是相当于在windows本地一样，在你的Linux 本地可以分，但外网（你的电脑还访问不了）。最终的目标是pycharm客户端直接输入链接地址，就可以激活。 此时需要用nginx，通过Linux的IP，接受你笔记本电脑IDE的请求，然后给Linux服务器的IdeaServer程序去处理激活。（反向代理的过程）

四.nginx 反向代理
------------

    有的小伙伴可能不懂为什么要弄nginx，上面都在云服务器运行了，直接ip:port访问不行吗？

当然不行，前面运行的脚本程序，是相对于在云服务器的本地 127.0.0.1:port 运行的（跟你在window本地差不多）。 外面的人想要访问肯定是要通过外网（云服务器的IP）的嘛

可通过外网IP进来，怎么知道你运行的程序端口在哪（前面的端口是本地端口），你得告诉人家啊，这里用nginx（你设置好了，nginx就帮你去处理），就像个迎宾小姐，接待访问，到你本地程序端口

这里为了方便，使用了基于域名的访问,（就是将你的外网IP绑定到 xxx.xxx.xxx 的域名），然后访问域名 就是访问你的IP的对应服务。

如果你没有域名，最好申请一个，也不贵（或者配置基于IP的nginx 反向代理服务器）。  

下面使用宝塔面板，进行简单快速配置。无需了解nginx参数原理。[链接地址](%20https://www.bt.cn/register.html?referee=35684)

玩vps的不知道宝塔面板的，可以自己百度，安装上。直接点击操作，很方便

**0 安装web服务nginx(用于反向代理)**

进入宝塔面板后，会提示你安装web服务，选左边的安装就行，他就自己安装nginx。可能需要十几分钟

安装完进行下面的操作

**1 点宝塔页面的网站，先添加一个站点：如下**

**安装完后创建一个站点，域名填准备的**

[![image](https://img2018.cnblogs.com/blog/1165731/201811/1165731-20181111174833566-126717267.png "image")](https://img2018.cnblogs.com/blog/1165731/201811/1165731-20181111174832022-1726154371.png)

[![18-11-11_15-17-32](https://img2018.cnblogs.com/blog/1165731/201811/1165731-20181111174834984-474329580.png "18-11-11_15-17-32")](https://img2018.cnblogs.com/blog/1165731/201811/1165731-20181111174834064-641394118.png)

**2.设置反向代理**

[![image](https://img2018.cnblogs.com/blog/1165731/201811/1165731-20181111174836269-1995098109.png "image")](https://img2018.cnblogs.com/blog/1165731/201811/1165731-20181111174835749-1927907137.png)

目标url ---> [http://127.0.0.1:6789](http://127.0.0.1:6789)   6789 填写你自己前面运行脚本的端口号

[![18-11-11_16-19-06](https://img2018.cnblogs.com/blog/1165731/201811/1165731-20181111174839019-226046874.png "18-11-11_16-19-06")](https://img2018.cnblogs.com/blog/1165731/201811/1165731-20181111174838036-1196245747.png)

下面是手动配置反向代理的 nginx.conf 文件（不懂就不用管）

```
worker_processes  1;
events {
    worker_connections  1024;
}
http {
    include       mime.types;
    default_type  application/octet-stream;
    sendfile        on;
    keepalive_timeout  65;
   server{

    listen 80;
    server_name idea.xxxxxx.com;     # 准备好的域名，没有的话直接写 127.0.0.1，到时候激活时填写你服务器的IP
    index index.php index.html index.htm default.php default.htm default.html;
    root /www/wwwroot/idea.wenyule.com;

   location / {

    　　proxy_pass http://127.0.0.1:1029;  #指定监听的端口


    　　proxy_redirect off;
   　　 proxy_set_header Host $host;
   　　 proxy_set_header X-Real-IP $remote_addr;
    　　proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
   　　 }
   　　 access_log  /www/wwwlogs/idea.wenyule.com.log;
    　　error_log  /www/wwwlogs/idea.wenyule.com.error.log;
    }
}


```
反向代理

 然后访问你的域名看反向代理是否成功，出现not found 就是成功了（因为你没有设置静态页面，所以not found）

[![image](https://img2018.cnblogs.com/blog/1165731/201811/1165731-20181111174840638-1061904893.png "image")](https://img2018.cnblogs.com/blog/1165731/201811/1165731-20181111174840087-1138365651.png)

 最后就是输入你的服务器地址 例如，http://idea.xxxx.com

 ![](https://img2018.cnblogs.com/blog/1165731/201810/1165731-20181014173520776-1976211018.png)

嫌麻烦的或追求新的版本的idea,可以下载crack 脚本的方式激活，对使用并没有什么影响

[本文连接：](https://www.cnblogs.com/wenyule/p/ideaserver.html)