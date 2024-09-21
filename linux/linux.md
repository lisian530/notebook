# linux文件基本属性
 - chown 修改所属用户与组
 - chmod 修改用户的权限
 - ll/ls-l 显示文件的属性和所属用户和组


```bash
[root@www /]# ls -l
total 64
dr-xr-xr-x   2 root root 4096 Dec 14  2012 bin
dr-xr-xr-x   4 root root 4096 Apr 19  2012 boot
```
- d 目录
- -文件
- l 链接文档
- b 装置文件里面的可供储存的接口设备(可随机存取装置)
- c 装置文件里面的串行端口设备，例如键盘、鼠标(一次性读取装置)
- r 可读
- w 可写
- x 执行
![alt text](images/image-1.png)
>这三个权限的位置不会改变，如果没有权限，就会出现减号 - 而已。

![alt text](images/image-2.png)

- 第 1-3 位确定属主（该文件的所有者）拥有该文件的权限
- 第4-6位确定属组（所有者的同组用户）拥有该文件的权限
- 第7-9位确定其他用户拥有该文件的权限
- *第 1、4、7 位读权限， r ，则有读权限， - 字符，则没有读权限*
- *第 2、5、8 位写权限， w ，则有写权限， - 字符, 没有写权限*
- *第 3、6、9 位可执行权限， x ，则有执行权限，- 字符，则没有执行权限。*
***
# ***Linux文件属主和属组***
```bash
[root@www /]# ls -l
total 64
drwxr-xr-x 2 root  root  4096 Feb 15 14:46 cron
drwxr-xr-x 3 mysql mysql 4096 Apr 21  2014 mysql
```
#
# *更改文件属性*
1. ***chgrp：更改文件属组***

```bash
chgrp [-R] 属组名 文件名
```
>-R：递归更改文件属组 (该目录下的所有文件的属组都会更改。)


2. *chown：更改文件所有者（owner），也可以同时更改文件所属组*
```bash
chown [–R] 所有者 文件名
chown [-R] 所有者:属组名 文件名
```
- 进入 /root 目录（~）将install.log的拥有者改为bin这个账号
```bash
[root@www ~] cd ~
[root@www ~]# chown bin install.log
[root@www ~]# ls -l
-rw-r--r--  1 bin  users 68495 Jun 25 08:53 install.log
```
- 将install.log的拥有者与群组改回为root
```bash
[root@www ~]# chown root:root install.log
[root@www ~]# ls -l
-rw-r--r--  1 root root 68495 Jun 25 08:53 install.log
```
3. *chmod：更改文件9个属性*

>Linux文件属性有两种设置方法，一种是数字，一种是符号



- Linux文件的基本权限
（owner/group/others(拥有者/组/其他)； read/write/execute 的权限。 ）
>-rwxrwxrwx
- r:4
- w:2
- x:1

- ***每种身份(owner/group/others)各自的三个权限(r/w/x)分数是需要累加的***

1. owner = rwx = 4+2+1 = 7
2. group = rwx = 4+2+1 = 7
3. others= --- = 0+0+0 = 0

* 变更时，该文件的权限数字就是 770；变更权限的指令 chmod 的语法
```bash
 chmod [-R] xyz 文件或目录
 ```
* 选项与参数:
1. xyz :刚刚提到的数字类型的权限属性，为 rwx 属性数值的相加
2. -R : 进行递归(recursive)的持续变更，以及连同次目录下的所有文件都会变更
* -R : 进行递归(recursive)的持续变更，以及连同次目录下的所有文件都会变更
```bash
[root@www ~]# ls -al .bashrc
-rw-r--r--  1 root root 395 Jul  4 11:45 .bashrc
[root@www ~]# chmod 777 .bashrc
[root@www ~]# ls -al .bashrc
-rwxrwxrwx  1 root root 395 Jul  4 11:45 .bashrc
```
>那如果要将权限变成 -rwxr-xr-- (权限的分数就成为 [4+2+1][4+0+1][4+0+0]=754)
***

# *符号类型改变文件权限*
- user：用户
- group：组
- others：其他

|     |      |      |       |       |
| ----- | ----- | ----- | ----- | ----- |    
| chmod | u     | +(加入)|  r   |  文件或目录
| chmod | g     | -(除去)|  w   |  文件或目录
| chmod | o     | =(设定)|  x   |  文件或目录
| chmod | a     |        |      |  文件或目录


* 将文件权限设置为 -rwxr-xr-- ，可以使用 chmod u=rwx,g=rx,o=r 文件名:
```bash
#  touch test1    // 创建 test1 文件
# ls -al test1    // 查看 test1 默认权限
-rw-r--r-- 1 root root 0 Nov 15 10:32 test1
# chmod u=rwx,g=rx,o=r  test1    // 修改 test1 权限
# ls -al test1
-rwxr-xr-- 1 root root 0 Nov 15 10:32 test1
```
* 而如果是要将权限去掉而不改变其他已存在的权限呢？例如要拿掉全部人的可执行权限:
```bash
#  chmod  a-x test1
# ls -al test1
-rw-r--r-- 1 root root 0 Nov 15 10:32 test1
```
***











