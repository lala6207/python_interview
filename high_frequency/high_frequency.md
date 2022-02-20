#### 1.什么是WSGI？

指定了web服务器和web框架/web应用程序之间的建议的标准接口。以促进web程序在各种web服务器之间的移植性。

WSGI协议主要包括Server和Apllication两部分： 

Server负责接受客户端请求并解析，将请求转发给Apllication,然后把Apllication的Response转发给客户端。

Application接受由Server转发的请求，处理请求，并将结果转发给Server。
Application可以包含多个中间件，并同时包含Server和Application。

WSGI协议其实定义了一种Server与Application解耦的规范。即可以有多个实现WSGI的服务器，也可以有多个实现WSGI的Application的框架。
那么就可以选择任意的Server和Application实现Web框架。
例如uWSGI和Gunicorn都是实现了WSGI的Server的服务器。
Django和Flask都是实现了WSGI的Application的Web框架。

相比之下，尽管Java有同样多的Web框架可用，但Java的Servlet API使得任何使用 Java Web 应用程序框架编写的应用程序可以在任何支持 servlet API 的 Web 服务器上运行。

#### 2.CGI和FastCGI的区别？

CGI:存放在 HTTP服务器上，为用户和http服务器之外的其他应用程序提供互相“交谈”的软件。

FastCGI:不会每来一个请求，就fork一个进程，而是预先fork出更多的进程。并且实现了一个进程池。  

#### 3.uwsgi和gunicorn区别？  


#### 4.介绍一下Supervisor？
Supervisor 英 /ˈsuːpəvaɪzə(r)/ n. 监督者，管理者；
Supervisor（http://supervisord.org/）是用Python开发的一个client/server服务，是Linux/Unix系统下的一个进程管理工具，不支持Windows系统。它可以很方便的监听、启动、停止、重启一个或多个进程。用Supervisor管理的进程，当一个进程意外被杀死，supervisort监听到进程死后，会自动将它重新拉起，很方便的做到进程自动恢复的功能，不再需要自己写shell脚本来控制。

Supervisor管理进程是通过fork/exec的，这些被管理的进程，当做子进程启动。这样的话，只要在Supervisor的配置文件中，把要管理的进程的可执行路径写进去就OK。

当子进程挂掉的话，父进程可准确获取子进程信息，当然可对挂掉的子进程进行重启，重启不重启，要看配置文件的配置autostart=True。

Supervisor通过INI格式进行配置文件。

Supervisor常用命令:     
supervisorctl status        //查看所有进程的状态  
supervisorctl stop es       //停止es  
supervisorctl start es      //启动es  
supervisorctl restart es     //重启es  
supervisorctl update        //配置文件修改后使用该命令加载新的配置  
supervisorctl reload        //重新启动配置中的所有程序

##### 5.docker和vmare的区别？
1.docker是基于操作系统来实现的，而虚拟机是基于硬件来实现的。  
2.更快速的交付和部署。一次创建，到处运行。内核级虚拟化。更轻松的迁移和扩展，在任意平台运行（公有云，私有云，物理机，虚拟机，服务器）  
特性          容器          虚拟机     
启动          秒级          分钟级  
硬盘使用       一般为MB      一般为GB     
性能          接近原生        弱于原生  
系统支持量     单机支持上千个容量     一般是十几个   

3.Docker的核心技术？  
namespaces  
是linux提供的用于分离进程树，网络接口，挂载点以及进程间通信等的资源方法，  
linux的命名空间提供了7种不同的命名空间方式，可以设置新进程在那些资源上与宿主机隔离。  

controlgroups
命名空间解决了进程，网络以及文件系统的隔离。
cgroups实现了CPU，内存等资源的隔离。

#### 6.类中的魔术方法？
在python类里面提供的，两个下划线开始，两个下划线结束。就叫做魔术方法。  
详解：https://blog.csdn.net/weixin_53501217/article/details/111675792
类在实例化对象的时候函数的调用顺序依次是__call__==>__new__==>__init__  
__call__：一个可调用的对象加括号,就是触发这个对象所在类中的__call__方法的执行  
__new__： 用来创建对象的  
__init__： 用来初始化实例变量的   
一个类在实例化时，实际做了三件事：  
1.触发元类中的__call__方法。  
2.通过__new__创建空对象。   
3.通过__init__初始化这个对象。  
4.返回这个对象。  





