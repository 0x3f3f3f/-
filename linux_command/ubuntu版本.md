## ubuntu版本

cat /etc/issue

![image-20220922184855607](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220922184855607.png)



## 通过名字查看运行的进程

ps aux | grep dbackup3

![image-20220922185058600](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220922185058600.png)



## 开启dbackup3服务器的命令

/etc/init.d/dbackup3-backupd start  // 也可以restart

/etc/init.d/dbackup3-agent start

## 查看日志

less  var/log/dbackup3/backupd.log



## 根据进程名字关掉进程

killall dbackup3-backupd

## ![image-20220922210320385](https://zhanghao1004.oss-cn-hangzhou.aliyuncs.com/image-20220922210320385.png)



