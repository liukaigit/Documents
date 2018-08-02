### Docker容器常用命令
- 测试环境
  - 宿主机linux（centos），测试目录：`/usr/share/tmp/`
- 基础镜像信息如下：
  ```
  REPOSITORY      TAG       IMAGE ID       CREATED       SIZE
  testdk          1.0.0     6bffbb33640c   2 hours ago   721.9 MB
  ```
- 该镜像容器运行信息
  ```
  CONTAINER ID     IMAGE          COMMAND       CREATED         STATUS         PORTS    NAMES
  cf62248785ba     testdk:1.0.0   "/bin/bash"   7 seconds ago   Up 5 seconds            mylk
  ```
  
**1、查看**
- 查看镜像
  - `docker images`
- 查看运行容器
  - `docker ps -a` 
  - 参数`-a`可查看历史运行容器信息
- 查看指定镜像信息
  - `docker inspect [REPOSITORY]:[TAG]或[IMAGE ID]`
  
**2、备份**
- 镜像备份
  - `docker tag [REPOSITORY_OLD]:[TAG_OLD] [REPOSITORY_NEW]:[TAG_NEW]`  
  
**3、运行**
- 基于镜像启动容器
  - `docker run -ti --name="mydocker" -v 宿主即目录:容器虚拟目录 [REPOSITORY]:[TAG] /bin/bash`
  - 参数`-t`表示生成伪终端，`-i`交互模式运行
  - 参数`--name=`指定容器运行名称
  - 参数`-v`建立容器和宿主机之间映射关系目录
  - 运行上述命令进入容器终端，`exit`可退出容器
  
**4、镜像**
- 生成容器镜像，容器运行过程中，在宿主机运行如下命令生存镜像
  - `docker commit -m="提交信息" -a="提交者" [CONTAINER ID] [REPOSITORY_NEW]:[TAG_NEW]`
  
**5、删除**
- 删除镜像（删除某个多余的TAG）
  - `docker rmi [REPOSITORY]:[TAG]或[IMAGE ID]`
- 删除容器
  - `docker rm [CONTAINER ID]`
