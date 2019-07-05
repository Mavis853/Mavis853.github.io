# CentOS7安装MySQL
1. 在CentOS中安装及配置MYSQL。
2. 了解和修改MYSQL安全配置选项。

准备：

1. Centos7虚拟机（使用的是图形界面）
2. 官网下载 mysql-8.0.16-linux-glibc2.12-x86_64.tar

## 安装步骤：

1. 把 mysql-8.0.16-linux-glibc2.12-x86_64.tar 复制到虚拟机上
2. 运用查找命令找到Mysql文件：[root@localhost ~]# find / -name "*.tar"



3. 进入文件所在目录，解压缩包：

[root@localhost ~]# cd /root/.cache/vmware/drag_and_drop/JffXB7

[root@localhost JffXB7]# tar -xvf mysql-8.0.16-linux-glibc2.12-x86_64.tar

4. #给包重命名为mysql,并安装到/usr/local/目录下 mv mysql-8.0.16-linux-glibc2.12-x86_64 /usr/local/mysql
5. 查看mysql目录下的文件


6. 检查mysql组和用户是否存在，如无创建

   cat /etc/group | grep mysql 

   cat /etc/passwd | grep mysql

7. 创建mysql用户组

   groupadd mysql
   
   useradd -g mysql mysql

8. 修改用户mysql的密码(密码自己设定)  

   passwd mysql

9. 更改所属的组和用户

   chown -R mysql mysql 
  
   chgrp -R mysql mysql

10. 进入mysql目录，创建data目录

     cd /usr/local/mysql
  
     mkdir data
  
     cd /usr/local/mysql/bin
  
     ./mysqld –initialize
 
11. 在在/etc/下创建创建my.cnf

     cd /etc/
     
     touch my.cnf
     
     vim my.cnf
     
     cat my.cnf
     
     在配置文件中添加配置
     

12. 修改config配置，修改SELINUX=disabled

    vi /etc/selinux/config
    
    修改mysql目录权限
    
   chown -R mysql:mysql /usr/local/mysql
   
13. 创建软连接(实现可直接命令行执行mysql)

    ln -s /usr/local/mysql/bin/mysql /usr/bin
   
    #mysqld配置,拷贝启动文件到/etc/init.d/下并重命令为mysqld
   
    cp /usr/local/mysql/support-files/mysql.server  /etc/init.d/mysqld
   
14. 增加执行权限

      chmod 755 /etc/init.d/mysqld
      
15. 检查自启动项列表中没有mysqld

    chkconfig --list mysqld
    
    #如果没有就添加mysqld
    
    chkconfig --add mysqld
    
 16. 设置开机启动
    
    chkconfig mysqld on
    
    #启动测试
    
    service mysqld start
    
    成功启动：
    
    







