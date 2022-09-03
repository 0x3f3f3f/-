# docker image和容器踩坑

## 步骤一：

# ![image-20220831112658042](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220831112658042.png)



+ 利用项目的dockerfile文件，拉去一个基础映像，并且执行相应的命令
+ -t代表tag，建立的映像名字

## 步骤二：

​	查看docker中已经存在的映像有哪些

![image-20220831113017421](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220831113017421.png)

+ 映像建立完，wsl和docker都会关闭，需要重新启动



## 步骤三：



![image-20220831133910157](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220831133910157.png)

+ 根据上面的仓库名字（映像名字）
+ 这句话的意思是创建一个名字叫做bustub的容器名字，根据new_bustub的映像 bash是你开启容器以后执行的命令，否则容器会快读的exit(0)，一直开不起来。

```sh
sudo docker container run -it -v /mnt/f/wsl_ubuntu_project/cmu15445/project1/bustub:/bustub --name=bustub_env bustub /bin/bash
```

+ 这才是真正把项目引进docker容器的正确方式，run等于create + 下面的start,-v后面的路径是你本机的项目文件的路径,  :/bustub是替换的文件名字，放在docker里面的根目录下创建的一个文件夹下面。 --name=bustub_env是新建容器的名字 bustub是你的映像的名字,最后的bin/bash打开容器执行的第一条指令，不然的话就会直接退出。

## 步骤四（开启docker容器，以及进入容器的命令）：

![image-20220831113310798](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220831113310798.png)

+ 容器建立以后没有开启容器，docker ps打印容器名字，然后开启对应容器。



进入容器：

sudo docker exec -it 容器id /bin/bash





LTAI5tL5esqJS84WXBuk9vhP
mfJySgQnLKmCV9W7cVLzZQk5kK5Nf4





