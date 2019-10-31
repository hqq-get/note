### 计划任务
####  at命令

```shell
at [option]...TIME
-l 查看
-f 指定at文件
-d 删除指定的作业，相当于atrm
-c 查看指定作业的具体内容
-q 指明队列
```
示例：

``` shell
~]# at now+2min
at> cat /etc/passwd
at>                                    #ctrl +d 保存退出
job 2 at Thu Oct 31 03:29:00 2019
[root@localhost ~]# at -l
1	Thu Oct 31 03:28:00 2019 a root
2	Thu Oct 31 03:29:00 2019 a root
```

``` shell
[root@localhost ~]# at now+2min
at> echo "111"
at> <EOT>                                           
job 5 at Thu Oct 31 03:44:00 2019
[root@localhost ~]# 
[root@localhost ~]# at -l
5	Thu Oct 31 03:44:00 2019 a root
[root@localhost ~]# 
[root@localhost ~]# at -d 5
[root@localhost ~]# at -l
[root@localhost ~]# 
```
~~~
[root@localhost ~]# at now+2min
at> echo "222"
at> <EOT>
job 6 at Thu Oct 31 03:46:00 2019
[root@localhost ~]# 
[root@localhost ~]# at -l
6	Thu Oct 31 03:46:00 2019 a root
[root@localhost ~]# at -c 6
~~~

==注意：作业执行结果是以邮件发送给提交作业的用户==

#### crontab 周期性任务计划
###### 服务程序
- cronle:主程序包，提供了crond守护进程及相关辅助工具
- 确保crond守护进程正常运行:systemctl status crond
###### cron任务分为两类：
- 系统cron任务：主要用于实现系统自身的维护
  - 手动编辑： /etc/crontab 文件
- 用户cron任务：用户自定义
  - 使用crontab命令管理配置文件

###### crontab的配置格式
``` shell
SHELL=/bin/bash
PATH=/sbin:/bin:/usr/sbin:/usr/bin
MAILTO=root


# For details see man 4 crontabs

# Example of job definition:
# .---------------- minute (0 - 59)
# |  .------------- hour (0 - 23)
# |  |  .---------- day of month (1 - 31)
# |  |  |  .------- month (1 - 12) OR jan,feb,mar,apr ...
# |  |  |  |  .---- day of week (0 - 6) (Sunday=0 or 7) OR sun,mon,tue,wed,thu,fri,sat
# |  |  |  |  |
# *  *  *  *  * user-name  command to be executed
```



