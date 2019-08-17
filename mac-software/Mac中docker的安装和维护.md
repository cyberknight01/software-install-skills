# # Docker 在mac上的安装维护学习
![屏幕快照 2019-08-17 下午9.15.57](media/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-08-17%20%E4%B8%8B%E5%8D%889.15.57.png)
## 跟新维护记录
```
2018-0114  
2019-0817维护重新安装镜像
```
可参考 []()http://www.secist.com/archives/4016.html

1，首先在mac上安装docker，可直接在网站下载

2，安装完之后，在mac终端中输入
```
docker version      显示 Docker 版本信息
docker info         显示 Docker 系统信息，包括镜像和容器数
docker images       查看当前的镜像
```
3，然后安装镜像，将开放的服务器上的 （镜像）images 安装到私有服务器上,命令如下
```
docker pull kalilinux/kali-linux-docker         将该linux镜像拉下
```
![屏幕快照 2019-08-17 下午1.14.39](media/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-08-17%20%E4%B8%8B%E5%8D%881.14.39.png)
4，镜像安装完之后，利用镜像创建一个dock实例，打开并运行一个容器
```
docker run -t -i  --name docker-kali kalilinux/kali-linux-docker /bin/bash
```
![屏幕快照 2019-08-17 下午1.36.02](media/%E5%B1%8F%E5%B9%95%E5%BF%AB%E7%85%A7%202019-08-17%20%E4%B8%8B%E5%8D%881.36.02.png)
5，在该容器下下载metasploit,此过程要耗费5分钟左右时间，视网速而定
```
apt-get update && apt-get install metasploit-framework
```
6，基本操作
```
docker start docker-kali或者容器id       打开容器
Docker attach docker-kali或者 容器id     连接容器 
exit                                    容器内退出 
docker stop docker-kali或者容器id        容器外退出
docekr ps -a -q                         查看容器停止或者正在运行的容器id
docker rm docker-kali或者 容器id         删除容器操作只能删除已经停止的容器
docker rm $(docker ps -a -q)           批量删除容器，意思是批量删除停止的容器
docker rmi 镜像名or镜像id                删除镜像，删除之前需停止容器并删除和该镜像关联的容器
docker rmi $(docker images -q)         批量删除所有的镜像
docker commit 容器名 镜像名              使用如下命令可以把一个正在运行的容器变成一个新的镜像
docker save -o 保存的文件名 镜像名        通过save命令将镜像打包成文件，拷贝给别人使用
eg:docker save -o ./kali.tar docker-kali
docker load -i ./kali.tar           对方在拿到镜像文件后，可以通过load方法，将镜像加载到本地
``` 
#### docker run中参数的意义
```
-i 表示以“交互模式”运行容器
-t 表示容器启动后会进入其命令行。加入这两个参数后，容器创建就能登录进去。即 分配一个伪终端。
--name 为创建的容器命名
-v 表示目录映射关系(前者是宿主机目录，后者是映射到宿主机上的目录，即 宿主机目录:容器中目录)，可以使 用多个-v 做多个目录或文件映射。注意:最好做目录映射，在宿主机上做修改，然后 共享到容器上。
-d 在run后面加上-d参数,则会创建一个守护式容器在后台运行(这样创建容器后不 会自动登录容器，如果只加-i -t 两个参数，创建后就会自动进去容器)。
-p 表示端口映射，前者是宿主机端口，后者是容器内的映射端口。可以使用多个-p 做多个端口映射
-e 为容器设置环境变量
--network=host 表示将主机的网络环境映射到容器中，容器的网络与主机相同
```
#### 查看运行和终止的容器
```
查看当前运行的 容器
docker ps -a 
列出本机正在运行的容器
docker container ls
列出本机所有容器，包括已经终止运行的
docker container ls --all
```
#### 停止与启动容器
```
停止一个已经在运行的容器
docker container stop 容器名或容器id
启动一个已经停止的容器
docker container start 容器名或容器id
kill掉一个已经在运行的容器
docker container kill 容器名或容器id
删除容器
docker container rm 容器名或容器id
```
#### 进入已经正在运行的容器
```
docker exec -it 容器名或容器id 进入后执行的第一个命令
eg:docker exec -it docker-kali /bin/bash
```
待安装docker-kali 里安装了一些安全测试软件
```
apt-get install websploit  arachni nikto sqlmap websploit nmap
```
-------
Perl   Mac 电脑已自带安装环境
[]()http://blog.csdn.net/andanlan/article/details/51589800

