# Linux cookbook
linux cookbook, linux烹饪书，linux命令总结，linux cli by example  
## 命令行移动
### Basic moves
Move back one character. Ctrl + b
Move forward one character. Ctrl + f
Delete current character. Ctrl + d
Delete previous character. Backspace
Undo. Ctrl + -

### Moving faster
Move to the start of line. Ctrl + a
Move to the end of line. Ctrl + e
Move forward a word. Meta + f (a word contains alphabets and digits, no symbols)
Move backward a word. Meta + b
Clear the screen. Ctrl + l

> What is Meta? Meta is your Alt key, normally. For Mac OSX user, you need to enable it yourself. Open Terminal > Preferences > Settings > Keyboard, and enable Use option as meta key. Meta key, by convention, is used for operations on word.

### Cut and paste (‘Kill and yank’ for old schoolers)
Cut from cursor to the end of line. Ctrl + k
Cut from cursor to the end of word. Meta + d
Cut from cursor to the start of word. Meta + Backspace
Cut from cursor to previous whitespace. Ctrl + w
Paste the last cut text. Ctrl + y
Loop through and paste previously cut text. Meta + y (use it after Ctrl + y)
Loop through and paste the last argument of previous commands. Meta + .

### Search the command history
Search as you type. Ctrl + r and type the search term; Repeat Ctrl + r to loop through results.
Search the last remembered search term. Ctrl + r twice.
End the search at current history entry. Ctrl + j
Cancel the search and restore original line. Ctrl + g

### Need more?
A comprehensive [bash editing mode cheatsheet](http://www.catonmat.net/blog/bash-emacs-editing-mode-cheat-sheet/) by Peteris Krumin (catonmat.net).
Vim users! Do you know you can switch to Vi-style editing mode? Here: [vi-style cheatsheet](http://www.catonmat.net/blog/bash-vi-editing-mode-cheat-sheet/).
Bash command line editing is actually handled by GNU Readline Library. So just dive into [Readline manual](http://www.gnu.org/software/readline/#Documentation) for everything else.

## 查看linux版本

``` zsh
root@1de774242804:/# cat /etc/issue   #方法一
Debian GNU/Linux 9 \n \l

root@1de774242804:/# cat /etc/issue.net   #方法二
Debian GNU/Linux 9
root@1de774242804:/# uname -a  #方法三
Linux 1de774242804 4.9.125-linuxkit #1 SMP Fri Sep 7 08:20:28 UTC 2018 x86_64 GNU/Linux
root@1de774242804:/# cat /proc/version  #方法四
Linux version 4.9.125-linuxkit (root@659b6d51c354) (gcc version 6.4.0 (Alpine 6.4.0) ) #1 SMP Fri Sep 7 08:20:28 UTC 2018
```

## 查看硬件信息
`lshw`命令可以查看硬件信息  

`lscpu`命令可以查看cpu信息
```
root@MNG-BC ➜  ~ lscpu
Architecture:          x86_64
CPU op-mode(s):        32-bit, 64-bit
Byte Order:            Little Endian
CPU(s):                12
On-line CPU(s) list:   0-11
Thread(s) per core:    2
Core(s) per socket:    6
Socket(s):             1
NUMA node(s):          1
Vendor ID:             GenuineIntel
CPU family:            6
Model:                 85
Model name:            Intel(R) Xeon(R) Platinum 8163 CPU @ 2.50GHz
Stepping:              4
CPU MHz:               2499.998
BogoMIPS:              4999.99
Hypervisor vendor:     KVM
Virtualization type:   full
L1d cache:             32K
L1i cache:             32K
L2 cache:              1024K
L3 cache:              33792K
NUMA node0 CPU(s):     0-11
Flags:                 fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single ibrs ibpb stibp kaiser fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx avx512f rdseed adx smap avx512cd xsaveopt xsavec xgetbv1
```


`cat /proc/cupinfo`可以查看cpu信息，每一个核心都会列出来，以`core id`区分
```
root@MNG-BC ➜  ~ cat /proc/cpuinfo
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 85
model name      : Intel(R) Xeon(R) Platinum 8163 CPU @ 2.50GHz
stepping        : 4
microcode       : 0x1
cpu MHz         : 2499.998
cache size      : 33792 KB
physical id     : 0
siblings        : 12
core id         : 0
cpu cores       : 6
apicid          : 0
initial apicid  : 0
fpu             : yes
fpu_exception   : yes
cpuid level     : 13
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov pat pse36 clflush mmx fxsr sse sse2 ss ht syscall nx pdpe1gb rdtscp lm constant_tsc rep_good nopl pni pclmulqdq ssse3 fma cx16 pcid sse4_1 sse4_2 x2apic movbe popcnt tsc_deadline_timer aes xsave avx f16c rdrand hypervisor lahf_lm abm 3dnowprefetch invpcid_single ibrs ibpb stibp kaiser fsgsbase tsc_adjust bmi1 hle avx2 smep bmi2 erms invpcid rtm mpx avx512f rdseed adx smap avx512cd xsaveopt xsavec xgetbv1
bugs            : cpu_meltdown spectre_v1 spectre_v2 spec_store_bypass l1tf
bogomips        : 4999.99
clflush size    : 64
cache_alignment : 64
address sizes   : 46 bits physical, 48 bits virtual
power management:
```


## 查看系统信息
使用`uname`命令可以查看系统信息，了解系统信息对安装软件很有帮助，安装软件时必须知道是装32位还是64位，是x86架构还是i686架构呢?  
mac示例  
``` bash
shiming@pro ➜  ~ uname -a
Darwin pro 18.2.0 Darwin Kernel Version 18.2.0: Fri Oct  5 19:41:49 PDT 2018; root:xnu-4903.221.2~2/RELEASE_X86_64 x86_64
```

ubuntu示例  
``` bash
root@MNG-BC ➜  ~ uname -a
Linux MNG-BC 4.4.0-142-generic #168-Ubuntu SMP Wed Jan 16 21:00:45 UTC 2019 x86_64 x86_64 x86_64 GNU/Linux
```

## 系统时间 - date

```
[shiming@red-hat-enterprise-linux ~]$ date        #打印系统时间
2018年 07月 25日 星期三 19:38:53 CST
[shiming@red-hat-enterprise-linux ~]$ date +%x    #打印日期
2018年07月25日
[shiming@red-hat-enterprise-linux ~]$ date --utc  #打印UTCtime
2018年 07月 25日 星期三 11:55:17 UTC
[shiming@red-hat-enterprise-linux ~]$ date +%T    #打印hh:mm:ss time
19:56:57
[shiming@red-hat-enterprise-linux ~]$ date +%s    #打印unix时间戳，精确到秒
1532519829
```

## 系统语言 - LANG
### 修改系统语言
```
[shiming@red-hat-enterprise-linux ~]$ cat /etc/locale.conf  #查看linux系统语言设置
LANG=en_US.UTF-8                                            #修改语言只需修改这行    
[shiming@red-hat-enterprise-linux ~]$ echo $LANG            #查看ssh语言环境变量设置
zh_CN.UTF-8                   #系统为英文，但ssh设置为中文，所以通过ssh远程连接还是会显示中文
[shiming@red-hat-enterprise-linux ~]$ LANG=en_US.UTF-8      #通过给LANG赋值改变ssh语言（这样只是临时修改，下次ssh登录时还是会显示中文）
```

### 使用本机或服务器语言
mac为例，在本机中 vi /etc/ssh/ssh_config,如果希望在ssh连接中传入loacle环境变量，则放开注释，否则用#号注释以下行（使用服务器的系统语言）
```
       SendEnv LANG LC_*
```

## 主机名 - hostnamectl
redhat中有三种主机名类型：--pretty, --static, and --transient， [参考1](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/sec_configuring_host_names_using_hostnamectl) and [参考2](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/7/html/networking_guide/ch-configure_host_names)
| Hostname Type | Description |
| -------- | -------- |
| Static     | Assigned by the system admin     |
| Transient/Dynamic     | Assigned by DHCP or mDNS server at runtime     |
| Pretty     | Assigned by the system admin. Its can be used as Description like “Oracle DB server”     |

### 查看和修改主机名
```
[shiming@red-hat-enterprise-linux ~]$ hostnamectl          #查看所有主机名
[shiming@red-hat-enterprise-linux ~]$ hostnamectl set-hostname redhat  #修改主机名（三个主机名都改为redhat）
[shiming@redhat ~]$                              #修改后重启，主机名变了
```

### 修改主机名(临时修改)
```
[shiming@red-hat-enterprise-linux ~]$ hostname            #查看主机名
red-hat-enterprise-linux.shared
[shiming@red-hat-enterprise-linux ~]$ hostname redhat     #修改主机名为redhat
hostname: you must be root to change the host name        #要root权限才能修改
[shiming@red-hat-enterprise-linux ~]$ sudo hostname redhat #使用管理员权限修改
[sudo] password for shiming: 
[shiming@red-hat-enterprise-linux ~]$ hostname            #查看修改后的主机名
redhat
                                                          #重启主机名不变
```
## 文件类型 -  file
Linux不以文件名后缀来识别文件类型，通过file命令可以查看文件类型，一般文件类型分为3类


| keyword | description |
| -------- | -------- |
| text    | 可读文本    |
| executable   | 可执行文件    |
| data    | 除此之外的叫做data，usually “binary” or non-printable |
```
[shiming@redhat ~]$ file /etc/passwd
/etc/passwd: ASCII text
[shiming@redhat ~]$ file /bin/passwd
/bin/passwd: setuid ELF 64-bit LSB shared object, x86-64, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.32, BuildID[sha1]=0a16a7915f7f9b01d96442755257e22067ce5b2c, stripped
```
## 文件统计 - wc
wc for word count, print newline, word, and byte counts for each file

```
[shiming@redhat ~]$ wc /etc/passwd        
  46  100 2426 /etc/passwd                  #行数，word数，byte数，文件名
[shiming@redhat ~]$ wc -l /etc/passwd       #只打印行数
46 /etc/passwd
```
## 磁盘使用情况
`df`显示磁盘使用情况，默认大小为bytes，加上`-h`参数使用更适于人类阅读的方式展示
```
root@mix2 ➜  bitcoin df -h
Filesystem      Size  Used Avail Use% Mounted on
udev             16G     0   16G   0% /dev
tmpfs           3.2G  4.6M  3.2G   1% /run
/dev/vda1        99G   45G   49G  48% /
tmpfs            16G   40K   16G   1% /dev/shm
tmpfs           5.0M     0  5.0M   0% /run/lock
tmpfs            16G     0   16G   0% /sys/fs/cgroup
/dev/vdc       1008G   63G  895G   7% /mnt/ethereum
/dev/vdb       1008G  273G  684G  29% /mnt/bitcoin
tmpfs           3.2G     0  3.2G   0% /run/user/0
tmpfs           3.2G     0  3.2G   0% /run/user/1002
```
## 文件大小
`du`命令查看文件大小, `du -h`, h means human readable,默认
```
root@mix2 ➜  bitcoin du --max-depth=0 -h
273G	.
root@mix2 ➜  bitcoin du --max-depth=1 -h
26G	./testnet3
26G	./omni
223G	./mainnet
273G	.
```

## 文件打印
### 开头 - head
默认打印开头10行
```
[shiming@redhat ~]$ head /etc/passwd        #头10行
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
sync:x:5:0:sync:/sbin:/bin/sync
shutdown:x:6:0:shutdown:/sbin:/sbin/shutdown
halt:x:7:0:halt:/sbin:/sbin/halt
mail:x:8:12:mail:/var/spool/mail:/sbin/nologin
operator:x:11:0:operator:/root:/sbin/nologin
```
可指定打印行数 - head -n [linenum]
```
[shiming@redhat ~]$ head -n 5 /etc/passwd    #头5行
root:x:0:0:root:/root:/bin/bash
bin:x:1:1:bin:/bin:/sbin/nologin
daemon:x:2:2:daemon:/sbin:/sbin/nologin
adm:x:3:4:adm:/var/adm:/sbin/nologin
lp:x:4:7:lp:/var/spool/lpd:/sbin/nologin
```

### 末尾 - tail

默认打印末尾10行
```
[shiming@redhat ~]$ tail /etc/passwd
nfsnobody:x:65534:65534:Anonymous NFS User:/var/lib/nfs:/sbin/nologin
pcp:x:990:985:Performance Co-Pilot:/var/lib/pcp:/sbin/nologin
gnome-initial-setup:x:989:984::/run/gnome-initial-setup/:/sbin/nologin
nslcd:x:65:55:LDAP Client User:/:/sbin/nologin
avahi:x:70:70:Avahi mDNS/DNS-SD Stack:/var/run/avahi-daemon:/sbin/nologin
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
oprofile:x:16:16:Special user account to be used by OProfile:/var/lib/oprofile:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
shiming:x:1000:1000:Shiming Liu:/home/shiming:/bin/bash
```
指定打印行数 - tail -n [linenum]
```
[shiming@redhat ~]$ tail -n 5 /etc/passwd
postfix:x:89:89::/var/spool/postfix:/sbin/nologin
sshd:x:74:74:Privilege-separated SSH:/var/empty/sshd:/sbin/nologin
oprofile:x:16:16:Special user account to be used by OProfile:/var/lib/oprofile:/sbin/nologin
tcpdump:x:72:72::/:/sbin/nologin
shiming:x:1000:1000:Shiming Liu:/home/shiming:/bin/bash
```

打印整个文件内容 - cat [filename]
```
[shiming@redhat ~]$ tail /etc/passwd
```

## 文件管理
### linux文件结构
***man自带帮助页：[man hier](https://www.systutorials.com/docs/linux/man/7-hier/)***
![](https://box.kancloud.cn/f075453374d52e3ae00def2b6c7a3a41_1182x648.png)

### 文件结构标准
Filesystem Hierarchy Standard
[fhs-2.3.pdf](http://www.pathname.com/fhs/pub/fhs-2.3.pdf)
http://www.pathname.com/fhs/

|位置	|用途|
| -------- | -------- |
|/usr |	安装软件、共享的库，包括文件和静态只读程序数据。重要的子目录有：</br> -/usr/bin：用户命令。</br> -/usr/sbin：系统管理命令。</br> -/usr/local：本地自定义软件。|
|/etc |	特定于此系统的配置文件, 静态的永久系统配置数据。|
| /var | 	特定于此系统的可变数据，在系统启动之间保持永久性。动态变化的文件（如数据库、缓存目录、日志文件、打印机后台处理文档内容和网站内容）可以在 /var 下找到。|
|/run	|包含动态的、非永久的应用程序运行时数据,自上一次系统启动以来启动的进程的运行时数据。这包括进程 ID 文件和锁定文件，等等。此目录中的内容在重启时重新创建。（此目录整合了旧版 Red Hat Enterprise Linux 中的 /var/run 和 /var/lock。）|
|/home	|普通用户主目录。|
|/root	|root 主目录。|
|/tmp	|临时文件目录。10 天内未访问、未更改或未修改的文件将自动从该目录中删除。还有一个临时目录 /var/tmp，该目录中的文件如果在 30 天内未曾访问、更改或修改过，将自动删除。|
|/boot	|开机启动过程中所需的文件。|
|/dev	|包含特殊的设备文件，供系统使用的物理硬件。|
|/media	|可移除的设备挂载点，如cd、vcd、U盘|
| /usr/bin    |  普通用户命令和实用程序     |
| /usr/sbin/     |  供root用户使用的二进制文件    |

### 打印当前工作目录
```
[shiming@redhat tmp]$ pwd
/tmp
```

### 新建目录 - mkdir
```
[shiming@redhat ~]$ mkdir tmp
[shiming@redhat ~]$ ls
Desktop  Documents  Downloads  Music  Pictures  Public  Templates  tmp  Videos
```

### 文件列表 - ls
```
[shiming@redhat ~]$ ls -l                               #长列表
[shiming@redhat ~]$ ls -a                               #显示包括隐藏文件
[shiming@redhat ~]$ ls -R                               #递归列表（包含子文件夹）
[shiming@redhat dir2]$ ls -alR /tmp/dir1                #可组合使用
/tmp/dir1:
total 12
drwxrwxr-x.  3 shiming shiming 4096 Jul 26 22:25 .
drwxrwxrwt. 14 root    root    4096 Jul 26 22:26 ..
drwxrwxr-x.  2 shiming shiming 4096 Jul 26 22:26 dir2

/tmp/dir1/dir2:
total 8
drwxrwxr-x. 2 shiming shiming 4096 Jul 26 22:26 .
drwxrwxr-x. 3 shiming shiming 4096 Jul 26 22:25 ..
-rw-rw-r--. 1 shiming shiming    0 Jul 26 22:26 file1
-rw-rw-r--. 1 shiming shiming    0 Jul 26 22:26 .file2
```

ls可以一次性列出几个文件夹中的文件
```
[shiming@redhat ~]$ ls -l Music Pictures Videos         #列出N个文件夹
Music:
total 0
-rw-rw-r--. 1 shiming shiming 0 Jul 27 23:25 song1.mp3
-rw-rw-r--. 1 shiming shiming 0 Jul 27 23:25 song2.mp3

Pictures:
total 0
-rw-rw-r--. 1 shiming shiming 0 Jul 27 23:26 snap1.jpg
-rw-rw-r--. 1 shiming shiming 0 Jul 27 23:26 snap2.jpg

Videos:
total 0
-rw-rw-r--. 1 shiming shiming 0 Jul 27 23:27 film1.avi
-rw-rw-r--. 1 shiming shiming 0 Jul 27 23:27 film2.avi
```
### 切换目录
```
[shiming@redhat tmp]$ cd /    
[shiming@redhat /]$ cd ~/tmp  
[shiming@redhat tmp]$ cd -      #切到上一个工作目录
/
[shiming@redhat /]$ 
[shiming@redhat ~]$ cd ..       #切到父目录
[shiming@redhat home]$ ls
lost+found  shiming
[shiming@redhat ~]$ cd ../..    #从当前位置上移两个级别
[shiming@redhat /]$ 
```

### 新建文件 - touch
```
[shiming@redhat tmp]$ touch tmp1     #tmp1不存在则新建，存在则将文件的时间戳更新为当前时间
```
新建多个文件
```
[shiming@redhat tmp]$ touch file1 file2
```


使用大括号新建多个文件
```
[shiming@redhat ~]$ touch file{1..5}       #如果文件名有规则的话可以这么建
[shiming@redhat ~]$ ls -l
-rw-rw-r--. 1 shiming shiming    0 Jul 28 09:41 file1
-rw-rw-r--. 1 shiming shiming    0 Jul 28 09:41 file2
-rw-rw-r--. 1 shiming shiming    0 Jul 28 09:41 file3
-rw-rw-r--. 1 shiming shiming    0 Jul 28 09:41 file4
-rw-rw-r--. 1 shiming shiming    0 Jul 28 09:41 file5
```
### 文件管理
|文件管理命令|	单一来源	|多来源
|-----|-----|-----|
|复制文件|	cp file1 file2|cp file1 file2 file3 dir④|
|复制文件(目标文件夹不存在)|	mkdir -p ~/.litecoin && cp bitcoin.conf litecin.conf|
|移动文件|	mv file1 file2①|	mv file1 file2 file3 dir④|
|删除文件|	rm file1|	rm -f file1 file2 file3⑤|
|创建目录|	mkdir dir|	mkdir -p part1/part2/dir⑥|
|复制目录|	cp -r dir1 dir2②|	cp -r dir1 dir2 dir3 dir4④|
|移动目录|	mv dir1 dir2③|	mv dir1 dir2 dir3 dir4④|
|删除目录|	rm -r dir1②|	rm -rf dir1 dir2 dir3⑤|
*注：	
①结果为重命名。
②需要使用“递归”选项来处理来源目录。
③如果 dir2 存在，则结果为移动。如果 dir2 不存在，则结果为重命名。
④最后一个参数必须是目录。
⑤请谨慎使用“force”选项，系统将不会提示您确认操作。
⑥**使用“创建父级”选项时应小心；无法捕获键入错误。**

### 文件链接
```
~/.oh-my-zsh/themes/
```

### 硬盘格式化和挂载
https://help.aliyun.com/document_detail/25426.html



### 远程文件传输
在本地terminal下执行scp命令
1. 将本地文件复制到远程
```
# 将本地文件file1.txt复制到远程服务器家目录下
$ scp file1.txt root@47.52.241.187:~
```

2. 将本地文件夹复制到远程(-r选项)
```
# 将本地文件夹dir1复制到远程家目录
$ scp -r dir1 root@47.52.241.187:~
```

3. 将远程文件复制到本地
```
# 将远程文件file2.txt 复制到本地工作目录
$ scp root@47.52.241.187:~/file2.txt .
```
4. 将远程文件夹复制到本地
```
# 将远程目录dir1复制到本地当前工作目录
$ scp -P <sshport> -r root@47.52.241.187:~/dir1 .
```
5. 将多个本地文件复制到远程
```
Shimings-Air:0-transfer Shiming$ scp file4 file5 root@47.52.241.187:~
# 只要输一次密码
Enter passphrase for key '/Users/Shiming/.ssh/id_rsa': 
file4                                         100%    0     0.0KB/s   00:00    
file5                                         100%    0     0.0KB/s   00:00
```

6. 将多个远程文件复制到本地
```
# 几个文件就输几次密码
Shimings-Air:~ Shiming$ scp root@47.52.241.187:~/{file1.txt,file2.txt} .
Enter passphrase for key '/Users/Shiming/.ssh/id_rsa': 
file1.txt                                     100%   26     0.3KB/s   00:00    
Enter passphrase for key '/Users/Shiming/.ssh/id_rsa': 
file2.txt                                     100%   26     0.3KB/s   00:00 
```

## 用户管理
### 添加用户
https://www.tecmint.com/add-users-in-linux/

### 修改用户
https://www.tecmint.com/usermod-command-examples/

### 修改密码 - passwd
```
[shiming@red-hat-enterprise-linux ~]$ passwd      #修改当前用户密码
更改用户 shiming 的密码 。
为 shiming 更改 STRESS 密码。
（当前）UNIX 密码：
新的 密码：
```

### 切换用户
`su` 切换到root用户
`su anotheruser` 将当前用户的环境变量带到新用户下
`su - anotheruser` 使用新用户的环境变量

### 禁止用户ssh登录
```
root@tool1:~# passwd -l bot  #-l means lock, lock后仍可以使用su - username切换用户
```

### 删除用户（连同用户home目录）
``` bash
deluser --remove-home tecmint      [On Debian and its derivatives]
userdel --remove tecmint           [On RedHat/CentOS based systems]
```
如果要更严谨的删除用户可以参考 https://www.tecmint.com/delete-remove-a-user-account-with-home-directory-in-linux/
1. 锁住账号，这样就无法登陆
2. 查看用户进程
3. 杀死用户进程
4. 备份用户家目录
5. 删除用户和家目录


## 软件安装
### 二进制包
```
tar xzf bitcoin-0.14.2-x86_64-linux-gnu.tar.gz
sudo install -m 0755 -o root -g root -t /usr/local/bin bitcoin-0.14.2/bin/*
```
-m 设置二进制文件权限
-o 设置owner
-g 设置group
-t 设置install目录
最后一个目录为源目录


## 命令替换

当命令包含反引号（注意，不是单引号），或$(command)时，允许命令替换
```
[shiming@redhat ~]$ echo today is `date +%A`    #反引号和单引号容易引起混淆
today is Saturday
[shiming@redhat ~]$ echo today is $(date +%A)   #建议使用$(command)
today is Saturday
```

## 命令历史
### 打印命令行历史
```
[shiming@redhat ~]$ history
  189  wc -l /etc/passwd
  190  man wc
  191  ls /etc/passwd
  192  su
  193  history
  194  ls /etc/passwd
  195  mkdir tmp
  196  ls /etc/passwd
  197  man wc
  198  history
```

### 执行历史命令行
```
  193  history
  194  ls /etc/passwd
  195  mkdir tmp
  196  ls /etc/passwd
  197  man wc
  198  history
[shiming@redhat ~]$ !194            #!+编号 可以执行历史命令行
ls /etc/passwd
/etc/passwd
[shiming@redhat ~]$ !m              #!+string 执行最近的一个以m开头的命令行，即 man wc
```

### 搜索命令历史
搜索`ctrl + r` , 取消搜索 `ctrl + g`

### 后台运行命令
nohup command &
``` bash
$ nohup geth --testnet --datadir /mnt/ethereum/ --syncmode "full" --rpc --ws &
```

如果要让正在运行的"前台任务"变为"后台任务"，可以先按ctrl + z，然后执行bg命令（让最近一个暂停的"后台任务"继续执行）

### 守护进程
http://www.ruanyifeng.com/blog/2016/02/linux-daemon.html

### systemd
http://www.ruanyifeng.com/blog/2016/03/systemd-tutorial-commands.html
systemd示例配置1
```
[Unit]
Description=ropsten
After=network.target
[Service]
Type=simple
LimitNOFILE=8192
WorkingDirectory=/mnt/disk2/ethereum/ropsten/
ExecStart=/usr/bin/geth --testnet --syncmode=full --datadir "/mnt/disk2/ethereum/ropsten" --rpc --rpcapi "eth,net,web3,admin,miner,debug,personal,txpool,db,shh" --rpccorsdomain '*' --rpcaddr 127.0.0.1 --rpcport 8540 --port 30300
Restart=always
User=bot
Group=bot
[Install]
WantedBy=multi-user.target
```

systemd示例配置2
```
[Unit]
Description=openresty A high performance web server and a reverse proxy server
After=network.target

[Service]
Type=forking
PIDFile=/usr/local/openresty/nginx/logs/nginx.pid
ExecStartPre=/usr/local/openresty/nginx/sbin/nginx -t -q -g 'daemon on; master_process on;'
ExecStart=/usr/local/openresty/nginx/sbin/nginx -g 'daemon on; master_process on;'
ExecReload=/usr/local/openresty/nginx/sbin/nginx -g 'daemon on; master_process on;' -s reload
ExecStop=-/usr/local/openresty/nginx/sbin/start-stop-daemon --quiet --stop --retry QUIT/5 --pidfile /run/nginx.pid
TimeoutStopSec=5
KillMode=mixed

[Install]
WantedBy=multi-user.target
```

新增一个service后来设置开机启动
每一个 Unit 都有一个配置文件，告诉 Systemd 怎么启动这个 Unit 。

Systemd 默认从目录/etc/systemd/system/读取配置文件。但是，里面存放的大部分文件都是符号链接，指向目录/usr/lib/systemd/system/，真正的配置文件存放在那个目录。

systemctl enable命令用于在上面两个目录之间，建立符号链接关系。
```
$ sudo systemctl enable clamd@scan.service
# 等同于
$ sudo ln -s '/usr/lib/systemd/system/clamd@scan.service' '/etc/systemd/system/multi-user.target.wants/clamd@scan.service'
```
如果配置文件里面设置了开机启动，systemctl enable命令相当于激活开机启动。

与之对应的，systemctl disable命令用于在两个目录之间，撤销符号链接关系，相当于撤销开机启动。
```
$ sudo systemctl disable clamd@scan.service
```

列出所有配置文件
```
# 列出所有配置文件
$ systemctl list-unit-files

# 列出指定类型的配置文件
$ systemctl list-unit-files --type=service
```

这个命令会输出一个列表
```
$ systemctl list-unit-files

UNIT FILE              STATE
chronyd.service        enabled
clamd@.service         static
clamd@scan.service     disabled
```

这个列表显示每个配置文件的状态，一共有四种。
```
enabled：已建立启动链接
disabled：没建立启动链接
static：该配置文件没有[Install]部分（无法执行），只能作为其他配置文件的依赖
masked：该配置文件被禁止建立启动链接
# 注意，从配置文件的状态无法看出，该 Unit 是否正在运行。这必须执行前面提到的systemctl status命令。
```

启动服务
```
systemctl start xxx.service
```

查看服务状态
```
systemctl status xxx.service
```

reload systemctl配置
```
systemctl daemon-reload  #一旦修改配置文件，就要让 SystemD 重新加载配置文件，然后重新启动，否则修改不会生效。
```

重启服务
```
systemctl restart xxx.service
```

停止服务
```
systemctl stop xxx.service
```

看所有systemctl的日志(启动失败的时候可以来这里看)
```
journalctl -xef
```

看指定service的日志
```
journalctl -u servicename
```

## 网络

端口号说明：
| 端口号 | 说明 | 
| -------- | -------- | 
| 0~1023     | the Well Known Ports, also referred to as System Ports.     | 
| 1024~49151     | the Registered Ports, also known as User Ports.     | 
| 49152~65535     | the Dynamic Ports, also referred to as the Private Ports.     | 


查看服务和端口绑定信息：
``` bash
$ cat /etc/services
```

列出所有打开的端口或正在运行的端口（包括TCP/UDP）:
-l – prints only listening sockets
-n – shows port number
-t – enables listing of tcp ports
-u – enables listing of udp ports
``` bash
$ netstat -lntu
Active Internet connections (only servers)
Proto Recv-Q Send-Q Local Address           Foreign Address         State
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN
tcp        0      0 0.0.0.0:18333           0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:8545          0.0.0.0:*               LISTEN
tcp        0      0 127.0.0.1:8546          0.0.0.0:*               LISTEN
tcp6       0      0 :::18333                :::*                    LISTEN
tcp6       0      0 :::30303                :::*                    LISTEN
udp        0      0 0.0.0.0:68              0.0.0.0:*
udp        0      0 172.31.42.181:123       0.0.0.0:*
udp        0      0 127.0.0.1:123           0.0.0.0:*
udp        0      0 0.0.0.0:123             0.0.0.0:*
udp6       0      0 :::30303                :::*
udp6       0      0 :::123                  :::*
```

或使用 ss -lntu
``` bash
$ ss -lntu
Netid State      Recv-Q Send-Q              Local Address:Port                             Peer Address:Port
udp   UNCONN     0      0                               *:68                                          *:*
udp   UNCONN     0      0                   172.31.42.181:123                                         *:*
udp   UNCONN     0      0                       127.0.0.1:123                                         *:*
udp   UNCONN     0      0                               *:123                                         *:*
udp   UNCONN     0      0                              :::30303                                      :::*
udp   UNCONN     0      0                              :::123                                        :::*
tcp   LISTEN     0      128                             *:22                                          *:*
tcp   LISTEN     0      128                             *:18333                                       *:*
tcp   LISTEN     0      128                     127.0.0.1:8545                                        *:*
tcp   LISTEN     0      128                     127.0.0.1:8546                                        *:*
tcp   LISTEN     0      128                            :::18333                                      :::*
tcp   LISTEN     0      128                            :::30303                                      :::*
```

重启网络 - ubuntu
``` bash
sudo service networking restart
```
### 查看端口是否打开
1.你可以使用 lsof 命令来查看某一端口是否开放。查看端口可以这样来使用，我就以80端口为例：
lsof -i:80
如果有显示说明已经开放了，如果没有显示说明没有开放
2.netstat -aptn执行看看，是否监听在0.0.0.0:3306
3.
netstat -nupl (UDP类型的端口)
netstat -ntpl (TCP类型的端口)
例如
4.telnet ip  端口号   方式测试远程主机端口是否打开
参考：https://blog.csdn.net/m0_37975886/article/details/78405808?utm_source=copy 

### 防火墙

``` bash

root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw status verbose  #查看防火墙详情
Status: inactive  #未开启
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw allow 8545/tcp  #允许端口tcp访问
Rules updated
Rules updated (v6)
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw allow 8546/tcp
Rules updated
Rules updated (v6)
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw allow 8545/udp   #允许端口udp访问
Rules updated
Rules updated (v6)
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw allow 8546/udp
Rules updated
Rules updated (v6)
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw status verbose
Status: inactive
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw enable  #开启防火墙
Command may disrupt existing ssh connections. Proceed with operation (y|n)? y
Firewall is active and enabled on system startup
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw allow http #开启80端口(http)访问
Rule added
Rule added (v6)
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw allow https #开启443端口(https)访问
Rule added
Rule added (v6)
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw allow ssh #开启22端口(ssh)访问
Rule added
Rule added (v6)
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo service networking restart
root@iZj6c48apyeg9dvouqz3uxZ:~# sudo ufw status verbose
Status: active
Logging: on (low)
Default: deny (incoming), allow (outgoing), disabled (routed)
New profiles: skip

To                         Action      From
--                         ------      ----
8545/tcp                   ALLOW IN    Anywhere
8546/tcp                   ALLOW IN    Anywhere
8545/udp                   ALLOW IN    Anywhere
8546/udp                   ALLOW IN    Anywhere
80                         ALLOW IN    Anywhere
443                        ALLOW IN    Anywhere
22                         ALLOW IN    Anywhere
8545/tcp (v6)              ALLOW IN    Anywhere (v6)
8546/tcp (v6)              ALLOW IN    Anywhere (v6)
8545/udp (v6)              ALLOW IN    Anywhere (v6)
8546/udp (v6)              ALLOW IN    Anywhere (v6)
80 (v6)                    ALLOW IN    Anywhere (v6)
443 (v6)                   ALLOW IN    Anywhere (v6)
22 (v6)                    ALLOW IN    Anywhere (v6)
```

### 网络测试

``` bash
Shimings-Air:~ Shiming$ traceroute -p 8545 47.75.70.201
traceroute to 47.75.70.201 (47.75.70.201), 64 hops max, 52 byte packets
 1  172.16.0.1 (172.16.0.1)  4.037 ms  1.054 ms  1.719 ms
 2  192.168.5.1 (192.168.5.1)  5.688 ms  8.667 ms  6.993 ms
 3  100.64.0.1 (100.64.0.1)  16.788 ms  5.867 ms  7.902 ms
 4  213.106.38.59.broad.fs.gd.dynamic.163data.com.cn (59.38.106.213)  9.796 ms  8.975 ms  8.774 ms
 5  183.56.65.62 (183.56.65.62)  13.150 ms  10.301 ms
    183.56.65.66 (183.56.65.66)  11.280 ms
 6  59.43.80.21 (59.43.80.21)  12.356 ms  10.645 ms  11.649 ms
 7  59.43.130.106 (59.43.130.106)  12.012 ms  51.356 ms  43.798 ms
 8  59.43.187.126 (59.43.187.126)  16.115 ms
    59.43.187.122 (59.43.187.122)  13.389 ms
    59.43.187.150 (59.43.187.150)  11.819 ms
 9  59.43.187.178 (59.43.187.178)  16.522 ms
    59.43.183.106 (59.43.183.106)  21.514 ms
    59.43.188.126 (59.43.188.126)  18.220 ms
10  59.43.249.10 (59.43.249.10)  17.732 ms
    59.43.186.126 (59.43.186.126)  22.963 ms
    59.43.186.122 (59.43.186.122)  14.746 ms
11  210.48.139.70 (210.48.139.70)  21.244 ms
    210.48.136.158 (210.48.136.158)  19.783 ms
    203.100.48.254 (203.100.48.254)  22.733 ms
12  * * *
13  11.211.16.137 (11.211.16.137)  24.828 ms
    11.211.16.105 (11.211.16.105)  22.569 ms
    11.211.20.165 (11.211.20.165)  30.418 ms
14  * * *
15  * * *
16  * * *
17  * * *
```

### 查看网速
使用`nload`命令可以查看网络负荷，实时显示网速，按enter可以切换网卡  
`nload`比较简洁，只显示总网速，`nethogs`可以按进程显示网络占用，类似`htop`  

## 编辑命令行
分隔同一行中的命令

| shell命令 | 描述 |
| -------- | -------- |
| ctrl+a     | 跳到命令行开头     |
| ctrl+e     | 跳到命令行结尾     |
| ctrl+u     | 删除光标前内容     |
| ctrl+k     | 删除光标后内容     |
| ctrl+左箭头 | 向左跳一字        |
| ctrl+右箭头 | 向右跳一字        |
| ctrl+r | 在命令行历史中搜索某一模式命令 |
| ; | 分隔同一行中的命令        |
| Esc + . | 复制以前命令的最后一个参数     |

## bash配置文件
执行顺序： /etc/profile -> (~/.bash_profile | ~/.bash_login | ~/.profile) -> ~/.bashrc -> /etc/bashrc -> ~/.bash_logout  见[参考一](https://www.thegeekstuff.com/2008/10/execution-sequence-for-bash_profile-bashrc-bash_login-profile-and-bash_logout/)


|  file              | Interactive login | Interactive non-login |Script|Description|
| -------- | -------- | -------- | -------- | -------- |
|/etc/profile|A|||system wide version of ~/.profit, execute once when user login. Executed only for interactive shells|
|/etc/profile.d/\*|A|||user defined /etc/profile, invoked by /etc/profile|
|/etc/bashrc or /etc/bash.bashrc||A||system wide version of ~/.bashrc. Executed for both interactive and non-interactive shells. In fact in Ubuntu the /etc/profile calls the /etc/bashrc directly|
|~/.bashrc ||B||user defined shell config|
|~/.bash_profile |B1||||
|~/.bash_login |B2||||
|~/.profile |B3||||
|BASH_ENV  |||A||
|~/.bash_logout  |C||||

## 查看环境变量
查看所有环境变量使用printenv命令
`➜  ~ printenv`

## export
bash内建命令，使得子进程可以复用父进程的环境变量。通过命令行敲的export命令，不管是导入还是删除都是临时的。如果需要永久保持有效需要写在~/.bashrc等配置文件中。

## unset环境变量
`unset`命令可以删除export的环境变量
``` bash
➜  ~ export TMPVAR="XX"
➜  ~ printenv TMPVAR
XX
➜  ~ unset TMPVAR
➜  ~ printenv TMPVAR
```

## 查看单个环境变量
``` bash
➜  ~ printenv HOME
/Users/shiming
```

## 常见环境变量


| Variable | Description | 
| -------- | -------- |
| EDITOR     | The program to run to perform edits.     |
| HOME     | The Home directory of the user.     |
| LOGNAME     | The login name of the user.     |
| MAIL     | The location of the user's local inbox.     |
| OLDPWD     | The previous working directory.    |
| PATH     |A colon separated list of directories to search for commands.    |
| PAGER     | This program may be called to view a file.    |
| PS1     | PS1 The primary prompt string.    |
| PWD     | The present working directory.    |
| USER     | The username of the user.    |



### 参数说明
```
-p
List of all names that are exported in the current shell
-n
Remove names from export list
-f
Names are exported as functions
```

### export作用解析
没用export前
```
[shiming@redhat ~]$ name=shiming            #设置变量name=shimiing
[shiming@redhat ~]$ echo $name              #在当前进程下输出
shiming                                     #正确输出
[shiming@redhat ~]$ bash                    #新开一个进程
[shiming@redhat ~]$ echo $name              #在新开的进程输出$name
                                            #无效
[shiming@redhat ~]$ 
```

用了export后
```
[shiming@redhat ~]$ name=shiming            #设置变量name=shiming
[shiming@redhat ~]$ echo $name              #当前进程输出
shiming                                     #正确输出
[shiming@redhat ~]$ export name             #export变量
[shiming@redhat ~]$ bash                    #新开进程
[shiming@redhat ~]$ echo $name              #再次输出
shiming                                     #正确输出
```

### append to the PATH
给PATH加一个路径，用冒号分隔
```
$ export PATH=$PATH:/home/himanshu/practice/
```

### 固化环境变量
```
export name="xiongxiong"                        #在~/.bashrc文件末尾加上这句
[shiming@redhat shiming]$ echo $name            #打印为空

[shiming@redhat shiming]$ source .bashrc        #执行.bashrc
[shiming@redhat shiming]$ echo $name            #打印有值
xiongxiong
[shiming@redhat shiming]$ unset name            #如果不想用这个环境变量了，用unset暂时删除
[shiming@redhat shiming]$ echo $name            #打印为空

```

## 局部和全局环境变量设置
参考[这里](https://www.tecmint.com/set-unset-environment-variables-in-linux/)

## 进程管理
### 查看进程资源占用
使用命令`top`(或 `htop`，需要安装)
``` bash
Processes: 501 total, 2 running, 499 sleeping, 2532 threads                                              09:39:06
Load Avg: 2.68, 1.92, 1.79  CPU usage: 1.26% user, 1.42% sys, 97.30% idle
SharedLibs: 229M resident, 47M data, 86M linkedit.
MemRegions: 171203 total, 8320M resident, 84M private, 1873M shared.
PhysMem: 16G used (6889M wired), 118M unused.
VM: 2489G vsize, 1121M framework vsize, 30538579(0) swapins, 32834518(0) swapouts.
Networks: packets: 60080455/70G in, 68155895/7815M out. Disks: 6097134/243G read, 6811848/392G written.

PID    COMMAND      %CPU TIME     #TH    #WQ  #PORTS MEM    PURG   CMPRS  PGRP  PPID  STATE    BOOSTS
44018  top          5.0  00:02.23 1/1    0    26     6032K  0B     0B     44018 33399 running  *0[1]
44017  sleep        0.0  00:00.00 1      0    10     328K   0B     0B     26499 26726 sleeping *0[1]
44000  quicklookd   0.0  00:00.16 4      1    88     5104K  28K    0B     44000 1     sleeping  0[0]
43947  com.apple.iC 0.0  00:00.14 2      1    59     3032K  0B     256K   43947 1     sleeping  0[0]
43904  ocspd        0.0  00:00.02 2      1    36     1912K  0B     0B     43904 1     sleeping *0[1]
43881  Google Chrom 0.0  00:00.79 10     2    73     29M    4096B  9560K  1123  1123  sleeping *0[3]
43880  Google Chrom 0.0  00:05.02 16     1    125    98M    0B     19M    1123  1123  sleeping *0[3]
43879  Google Chrom 0.0  00:00.31 16     1    122    17M    0B     12M    1123  1123  sleeping *0[3]
43769  MTLCompilerS 0.0  00:00.06 3      3    27     16K    0B     10M    43769 1     sleeping  0[2]
43764  com.apple.pr 0.0  00:02.17 4      1    274    5948K  0B     21M    43764 1     sleeping *0[598]
43763  MTLCompilerS 0.0  00:00.07 3      3    27     12K    0B     10M    43763 1     sleeping  0[2]
43757  System Prefe 0.0  00:02.70 4      1    296    5632K  8192B  18M    43757 1     sleeping *0[304]
43729  com.apple.no 0.0  00:00.04 2      1    44     28K    0B     1424K  43729 1     sleeping  0[1]
43727  mdworker     0.0  00:00.07 3      1    54     52K    0B     3232K  43727 1     sleeping *0[1]
43711  Google Chrom 0.0  00:25.45 17     1    133    44M    0B     125M   1123  1123  sleeping *0[24]
43004  Google Chrom 0.2  04:07.35 19     1    150    208M   0B     62M    1123  1123  sleeping *0[26]
```
### 进程后台运行


| 命令 | 描述 | 
| -------- | -------- |
| command &     | 进程后台运行     |
| ctrl + c     | 停止前台运行进程     |
| ctrl + z     | 挂起当前进程     |
| bg     | 讲挂起的进程放在后台继续运行（需配合ctrl + z使用）     |
| bg [%num]    | 将进程放在后台运行     |
| fg [%num]    | 将进程放在前台运行     |
| kill -l    | 查看所有中断信号     |
| kill -9 pid    | 杀死进程     |
| jobs    | 查看jobs     |



### 查看指定进程
```
[shiming@redhat profile.d]$ ps -p 1        #查看pid = 1的进程信息
  PID TTY          TIME CMD
    1 ?        00:00:03 systemd
```

### 打印当前进程id
```
[shiming@redhat profile.d]$ echo $$        #两个美元符号打印当前进程名
19376
```

### 查询子进程信息
```
[shiming@redhat profile.d]$ echo $$        #当前进程
19376
[shiming@redhat profile.d]$ bash           #新起一个子进程
[shiming@redhat profile.d]$ echo $$        #获取子进程id
21139
[shiming@redhat profile.d]$ ps --ppid 19376  #查看子进程信息
  PID TTY          TIME CMD
21139 pts/0    00:00:00 bash
```

### 进程前台/后台运行切换
https://www.thegeekstuff.com/2010/05/unix-background-job/



### 查看

## vim
### 系统自带教程
```
[shiming@redhat ~]$ vimtutor
```
### vim复制内容到Mac系统剪贴板
mac自带的vim位于/usr/bin目录下，这个版本不支持将vim中的内容复制到系统剪贴板
如何查看是否支持复制到剪贴板：
```
vim --version
```
如果出现`+clipboard`则支持,出现`-clipboard`则不支持
所以需要自己重新安装vim, `brew install vim --with-client-server`  
安装后需要做两件事：
1. 做一个软连接到/usr/local/bin, 这样就会使用新装的vim，因为/usr/local/bin在path中比/usr/bin更靠前
```
ln -sf /usr/local/Cellar/vim/8.1.0600_1/bin/vim /usr/local/bin/vim
ln -sf /usr/local/Cellar/vim/8.1.0600_1/bin/vim /usr/local/bin/vi
```

2.还需要修改~/.vimrc文件，加上下面这行  
```
set clipboard=unnamed
```

以后就可以在vim中visual模式选中文字进行复制(yank)了

### 写read-only文件
有时没有用sudo打开文件，编辑后保存不了，会提示read-only，可以用以下命令将文件写进去，不用退出文件再sudo打开。  
``` zsh
:w !sudo tee %
```
命令解释：
:w – write
!sudo – call shell sudo command
tee – the output of write (:w) command is redirected using tee
% – current file name

### 常用命令列表

| 操作 | 命令 | 备注 |
| -------- | -------- | -------- |
| 光标左移    | h     |     |
| 光标右移    | l     |     |
| 光标下移    | j     |     |
| 光标上移    | k     |     |
| 插入模式    | i     |     |
| 附加模式    | a     |     |
| 复制行    | yy or Y     |     |
| 剪切行    | dd     |     |
| 剪切两行    | 2dd     |     |
| 粘贴（光标后）    | p     | p for paste    |
| 粘贴（光标前）    | P（大写）     |     |
| 复制行    | yy     |     |
| 显示行号    | :set number     |     |
| 不显示行号    | :set nonumber     |     |
| 显示所有设置项    | :set all     |     |
| 显示用户设置    | :set     |     |
| 删除到本单词结尾（包括紧跟着的空格）    | dw     |     |
| 删除到两个单词结尾（包括紧跟着的空格）    | d2w     | 以此类推    |
| 删除到本单词结尾（不包括紧跟的空格）    | de     |     |
| 删除到两个单词结尾（不包括紧跟的空格）    | d2e     | 以此类推    |
| 删除到本行末尾    | d$     |     |
| 删除到单词结尾并进入插入模式    | ce     | 方便修改该单词,c for change    |
| 删除到本行末尾并进入插入模式    | c$     | 方便修改单行    |
| 撤销    | u     |     |
| 撤销之撤销    | ctrl + r     | r for redo I think    |
| 保存    | :w     |     |
| 另存为    | :w + filename   | 将目前编辑的文件另存为filename    |
| 保存并退出    | :wq or :ZZ     |     |
| 不保存退出    | :q!     | q for quit    |
| 跳到词首    | w     | w for word    |
| 跳到下2个词首    | 2w     |  以此类推   |
| 跳到词尾    | e     | e for end    |
| 跳到下一词尾    | 2e     | 以此类推    |
| 光标回退    | b     | 回退一个词，到首字母    |
| 替换光标处字符    | r + <new_char>     |     |
| 找到该行第一个字母    | f + <char>     |     |
| 跳到文本末尾    | G     |     |
| 跳到文本开头    | gg     |     |
| 跳到指定行    | <line num> + G     |     |
| 向下搜索    | / + <key word>     |     |
| 向上搜索    | ？ + <key word>     |     |
| 查找下一个    | n     |     |
| 查找上一个    | N     |     |
| 跳到光标上一个所在的位置    | ctrl + o     | o for older    |
| 跳到光标下一个所在的位置    | ctrl + i     |     |
| 找到对称的另一半括号(大中小括号都行)    | 将光标置于括号上然后按%    |     |
| 替换光标行第一个匹配项    | :s/old/new/    |  old为待替换字符，new为新字符   |
| 替换光标行所有匹配项    | :s/old/new/g    |  g for global   |
| 替换指定行所有匹配项    | :#,#s/old/new/g    | 两个井号代表开始行和结束行    |
| 全局替换（无确认）    | :%s/old/new/g    |     |
| 全局替换（逐个确认）    | :%s/old/new/gc   | c for comfirm   |
| 执行外部命令     | :! + command   | 举例 :!ls  :!rm file |
| 进入visual模式     | v   | 进入visual模式后可以通过移动光标选中文字 |
| 复制选中文字     | visual模式选中 + y   |  |
| 删除选中文字     | visual模式选中 + d   |  |
| 选中文字另存为新文件     | visual模式选中 + :w + <filename>   |   |
| 在光标后插入另一文件的内容     | :r + filename   | 将filename附加到光标后  |
| 在光标后插入命令行的标准输出     | :r + !ls -l   | 将ls -l输出附加到光标后  |
| 在光标下插一空行     | o   | o for open, open a line |
| 在光标上插一空行     | O   |   |
| vim     | :set xxx   |         'ic' 'ignorecase'       ignore upper/lower case when searching <br/>'is' 'incsearch'        show partial matches for a search phrase <br/>'hls' 'hlsearch'        highlight all matching phrases <br/>给以上选项前加上'no'即可撤销命令 |
| 查看帮助    | :help   | 查看帮助时切换窗口ctrl + w |
| 个性化vim配置文件    | :e ~/.vimrc   | 查看帮助时切换窗口ctrl + w |


## 获取帮助
### 搜索帮助主题
```
[shiming@redhat ~]$ man -k passwd         #搜索与关键字passwd有关的帮助       
chpasswd (8)         - update passwords in batch mode
fgetpwent_r (3)      - get passwd file entry reentrantly
getpwent_r (3)       - get passwd file entry reentrantly
gpasswd (1)          - administer /etc/group and /etc/gshadow
grub2-mkpasswd-pbkdf2 (1) - Generate a PBKDF2 password hash.
kpasswd (1)          - change a user's Kerberos password
lpasswd (1)          - Change group or user password
lppasswd (1)         - add, change, or delete digest passwords.

```

### 帮助分类

|num |   topic | note
|----|----|---|
|      1|   Executable programs or shell commands | 用户命令
|      2|   System calls (functions provided by the kernel) | 系统调用
|      3|   Library calls (functions within program libraries) | 库函数
|      4|   Special files (usually found in /dev)|特殊文件
|      5|   File formats and conventions eg /etc/passwd | 文件格式
|      6|   Games | 游戏
|      7|   Miscellaneous (including macro packages and conventions), e.g. man(7), groff(7) | 惯例、标准和其他
|       8|   System administration commands (usually only for root)|系统管理命令
|       9|   Kernel routines [Non standard]|Linux内核API

### pinfo
pinfo提供更详细的帮助文档
```
[shiming@redhat doc]$ pinfo vim
```

### 查看软件包文档
软件包文档储存在/usr/share/doc目录下，里面包含大量软件包提供的文档说明


## 创建、查看和编辑文本文件
### 标准输入、标准输出、标准错误
![https://www.linuxunit.com/io-redirection-stdin-stdout-stderr-streams/](https://www.linuxunit.com/images/stdin-stdout-stderr.png)

### 重定向
#### stdout重定向，>覆盖写，>>追加写
```
[shiming@redhat doc]$ echo "hello" > /tmp/hello.txt         #输出重定向，新建
[shiming@redhat doc]$ cat /tmp/hello.txt
hello
[shiming@redhat doc]$ echo "world" >> /tmp/hello.txt        #输出重定向，追加 
[shiming@redhat doc]$ cat /tmp/hello.txt
hello
world
[shiming@redhat doc]$ echo "hello world" > /tmp/hello.txt   #输出重定向，覆盖
[shiming@redhat doc]$ cat /tmp/hello.txt
hello world
```

#### stderr重定向
```
[shiming@redhat doc]$ echox "hello world" 2>/tmp/hello_err.txt  #错误重定向，新建
[shiming@redhat doc]$ cat /tmp/hello_err.txt
bash: echox: command not found...
Similar command is: 'echo'
[shiming@redhat doc]$ echoy "hello world" 2>>/tmp/hello_err.txt #错误重定向，追加
[shiming@redhat doc]$ cat /tmp/hello_err.txt
bash: echox: command not found...
Similar command is: 'echo'
bash: echoy: command not found...
Similar command is: 'echo'
[shiming@redhat doc]$ echoz "hello world" 2 > /tmp/hello_err.txt #重定向符号左右不能空格
bash: echoz: command not found...
Similar command is: 'echo'
[shiming@redhat doc]$ echoz "hello world" 2>/tmp/hello_err.txt   #错误重定向，覆盖
[shiming@redhat doc]$ cat /tmp/hello_err.txt
bash: echoz: command not found...
Similar command is: 'echo'
[shiming@redhat doc]$ echoz "hello world" 2>/dev/null            #将错误信息重定向到/dev/null，从而将它丢弃
[shiming@redhat doc]$ cat /dev/null                              #无输出
```

#### stdout和stderr一起重定向
```
$ command >file 2>&1            #重定向stdout和stderr以覆盖同一个文件
$ command &>file                #与上面等效(推荐)

$ command >>file 2>&1           #重定向stdout和stderr以附加到同一个文件
$ command &>>file               #与上面等效(推荐)

#示例：
[shiming@redhat doc]$ echo "nice day" &>/tmp/nice.txt
[shiming@redhat doc]$ cat /tmp/nice.txt 
nice day
[shiming@redhat doc]$ echoa "nice day" &>>/tmp/nice.txt
[shiming@redhat doc]$ cat /tmp/nice.txt 
nice day
bash: echoa: command not found...
Similar command is: 'echo'
```

#### 重定向示例
##### 保存时间戳供以后参考
```
[shiming@redhat ~]$ date > /tmp/saved_timestamp
```
##### 将一个日志的后100行负责到另一文件
```
[shiming@redhat ~]$ tail -n 100 /var/log/dmesg >/tmp/last_100_boot_msg
```
##### 将四个文件连接为一个
```
[shiming@redhat ~]$ cat file1 file2 file3 file4 >/tmp/four_in_one
```
##### 将文件名列出到文件中
```
[shiming@redhat ~]$ cat /tmp/filename 
```
##### 将输出附加到现有文件
```
[shiming@redhat ~]$ echo "new line info" >>/tmp/many_lines_of_info
[shiming@redhat ~]$ diff previous_file current_file >>/tmp/tracking_change_made
```
##### 将错误重定向到文件
```
[shiming@redhat ~]$ find /etc -name passwd 2>/tmp/error
```
##### 将输出和错误分别定向到不同文件
```
[shiming@redhat ~]$ find /etc -name passwd >/tmp/output 2>/tmp/error
```
##### 忽略并丢弃错误信息
```
[shiming@redhat ~]$ find /etc -name passwd >/tmp/output 2>/dev/null
```
##### 将输出和错误信息一并保存
```
[shiming@redhat ~]$ find /etc -name passwd &>/tmp/save_both
```
##### 将输出和错误信息附加保存
```
[shiming@redhat ~]$ find /etc -name passwd &>>/tmp/save_both
```

### 管道
![](https://17fba4f9-a-62cb3a1a-s-sites.googlegroups.com/site/jocvlib/ethiopia/computer/linux/standard-linux-textbook/ch03/fig03-02.jpg?attachauth=ANoY7criN_2_KAHzVkRLkqXYnbO4nfF0VL9wd9AaWhPhLTk9fNbP9qMSGtlH-hi_ozjge_WCHA6WsdYnGYC84_U74BctPVnJPUsqL4pWhmHrrZalPOIiRbh-MkmNtdU-ndBNnQYYX0TecOBeCc2Jw1i9Usl-QgEwkQAmF_-pGmtadTsQ2czYxjTbRus437ntxO-VjW-iU6U1FDJW2CKMtG2WrbrJgw20R67mL8Efu4sB8RDgVJoRffDTz_IvqFHSlaKUYXLfzITurK8lw0d4g0ZBaxQJXpoy63BdamI7cVf4ZqEjdHTDfic%3D&attredirects=0)

#### 管道示例

##### 单一管道
```
[shiming@redhat ~]$ ls | wc -l            #计算文件数
14
```

##### 管道和重定向组合使用
```
#将ls -l命令输出前5行重定向到 /tmp.first_five_lines文件
[shiming@redhat ~]$ ls -l | head -n 5 > /tmp/first_five_lines  
[shiming@redhat ~]$ cat /tmp/first_five_lines 
total 36
drwxr-xr-x. 2 shiming shiming 4096 Mar  3 11:35 Desktop
drwxr-xr-x. 2 shiming shiming 4096 Jan 13  2018 Documents
drwxr-xr-x. 2 shiming shiming 4096 Jan 13  2018 Downloads
-rw-rw-r--. 1 shiming shiming    0 Jul 28 09:41 file1
```

##### tee
Copy standard input to each FILE, and also to standard output.
```
[shiming@redhat ~]$ ls -l file* | tee /tmp/saved_output   #文件中有保持，stdout也打印
-rw-rw-r--. 1 shiming shiming 0 Jul 28 09:41 file1
-rw-rw-r--. 1 shiming shiming 0 Jul 28 09:41 file2
-rw-rw-r--. 1 shiming shiming 0 Jul 28 09:41 file3
-rw-rw-r--. 1 shiming shiming 0 Jul 28 09:41 file4
-rw-rw-r--. 1 shiming shiming 0 Jul 28 09:41 file5
```

```
[shiming@redhat ~]$ ls -l file* | head -n 2 | tee /tmp/first_two_lines
-rw-rw-r--. 1 shiming shiming 0 Jul 28 09:41 file1
-rw-rw-r--. 1 shiming shiming 0 Jul 28 09:41 file2
```

## 用户和组
### 查看当前用户信息
```
[shiming@redhat ~]$ id
uid=1000(shiming) gid=1000(shiming) groups=1000(shiming),10(wheel) context=unconfined_u:unconfined_r:unconfined_t:s0-s0:c0.c1023
```

### passwd文件格式
![](https://www.cyberciti.biz/media/ssb.images/uploaded_images/passwd-file-791527.png)
1. **Username**: It is used when user logs in. It should be between 1 and 32 characters in length.
1. **Password**: An x character indicates that encrypted password is stored in /etc/shadow file. Please note that you need to use the passwd command to computes the hash of a password typed at the CLI or to store/update the hash of the password in /etc/shadow file.
1. **User ID (UID)**: Each user must be assigned a user ID (UID). UID 0 (zero) is reserved for root and UIDs 1-99 are reserved for other predefined accounts. Further UID 100-999 are reserved by system for administrative and system accounts/groups.
1. **Group ID (GID)**: The primary group ID (stored in /etc/group file)
1. **User ID Info**: The comment field. It allow you to add extra information about the users such as user’s full name, phone number etc. This field use by finger command.
1. **Home directory**: The absolute path to the directory the user will be in when they log in. If this directory does not exists then users directory becomes /
1. **Command/shell**: The absolute path of a command or shell (/bin/bash). Typically, this is a shell. Please note that it does not have to be a shell.

### 在passwd文件中搜索用户
搜索用户tom
```
$ grep tom /etc/passwd
```

### 组
与用户一样，组也有名称和编号（GID)。本地组在/etc/group中定义

#### 主要组
* 每个用户只有一个主要组
* 对于本地用户，主要组通过/etc/passwd第四个字段定义
* 通常，用户创建的新文件归主要组所有
* 通常，新建用户的主要组是名称与用户相同的新建组，用户是此用户专用组（UPG)的唯一成员

#### 补充组
用户可以是零个或多个补充组的成员。
属于本地组补充成员的用户列在/etc/group中组条目的最后一个字段中。对于本地组，成员身份由/etc/group中组条目的最后一个字段中的逗号分隔用户列表确定。


## 实用技巧
### ubuntu安装mysql
https://github.com/rackerlabs/rackspace-how-to/edit/master/content/cloud-servers/installing-mysql-server-on-ubuntu.md

### 配置mysql
https://github.com/rackerlabs/rackspace-how-to/edit/master/content/cloud-servers/configuring-mysql-server-on-ubuntu.md

### mysql开启远程连接
安装mysql后默认只支持127.0.0.1访问3306端口
``` bash
shiming@ubuntu:/etc/mysql/conf.d$ netstat -aptn
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:3306          0.0.0.0:*               LISTEN      -
tcp        0      0 10.1.1.236:22           10.1.1.232:50221        ESTABLISHED -
tcp        0      0 10.211.55.7:22          10.211.55.2:50237       ESTABLISHED -
tcp6       0      0 :::22                   :::*                    LISTEN      -
tcp6       0      0 ::1:631                 :::*                    LISTEN      -
```

要想让mysql listen 0.0.0.0:3306需要在其配置文件`/etc/mysql/mysql.conf.d/mysqld.cnf`找到`bind-address            = 127.0.0.1`改成 `bind-address            = 0.0.0.0` 这个操作需要管理员权限

然后重启mysql
`systemctl restart mysql`

再次查看端口状态，发现已经在监听0.0.0.0:3306了
``` bash
shiming@ubuntu:/etc/mysql/mysql.conf.d$ netstat -aptn
(Not all processes could be identified, non-owned process info
 will not be shown, you would have to be root to see it all.)
Active Internet connections (servers and established)
Proto Recv-Q Send-Q Local Address           Foreign Address         State       PID/Program name
tcp        0      0 127.0.1.1:53            0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:22              0.0.0.0:*               LISTEN      -
tcp        0      0 127.0.0.1:631           0.0.0.0:*               LISTEN      -
tcp        0      0 0.0.0.0:3306            0.0.0.0:*               LISTEN      -
```

试下使用外网地址连接
``` bash
shiming@ubuntu:/etc/mysql/mysql.conf.d$ mysql -h 10.211.55.7:3306 -u root -p
Enter password:
ERROR 2005 (HY000): Unknown MySQL server host '10.211.55.7:3306' (0)
shiming@ubuntu:/etc/mysql/mysql.conf.d$ mysql -h 10.211.55.7 -P 3306 -u root -p
Enter password:
ERROR 1130 (HY000): Host 'ubuntu.shared' is not allowed to connect to this MySQL server
```
发现失败了，第一个原因是不支持host:3306这样方式，需要用-h 10.211.55.7 -P 3306这样的方式，第二个原因是mysql的root账户只开启了localhost访问权限,登录后使用`SELECT host FROM mysql.user WHERE User = 'root';`命令可查看
``` bash
shiming@ubuntu:/etc/mysql/mysql.conf.d$ mysql -u root -p
Enter password:
Welcome to the MySQL monitor.  Commands end with ; or \g.
Your MySQL connection id is 6
Server version: 5.7.23-0ubuntu0.16.04.1 (Ubuntu)

Copyright (c) 2000, 2018, Oracle and/or its affiliates. All rights reserved.

Oracle is a registered trademark of Oracle Corporation and/or its
affiliates. Other names may be trademarks of their respective
owners.

Type 'help;' or '\h' for help. Type '\c' to clear the current input statement.

mysql> SELECT host FROM mysql.user WHERE User = 'root';
+-----------+
| host      |
+-----------+
| localhost |
+-----------+
1 row in set (0.00 sec)
```

新建一个mysql user赋予远程访问权限
``` sql
mysql> CREATE USER 'shiming'@'localhost' IDENTIFIED BY 'pass';
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON *.* TO 'shiming'@'localhost' WITH GRANT OPTION;
Query OK, 0 rows affected (0.00 sec)

mysql> CREATE USER 'shiming'@'%' IDENTIFIED BY 'pass';
Query OK, 0 rows affected (0.00 sec)

mysql> GRANT ALL PRIVILEGES ON *.* TO 'shiming'@'%' WITH GRANT OPTION;
Query OK, 0 rows affected (0.00 sec)

mysql> FLUSH PRIVILEGES;
Query OK, 0 rows affected (0.00 sec)
```

使用新建的用户登录，登录成功


### ubuntu下terminal复制/粘贴命令快捷键设置
Edit → Keyboard Shortcuts menu. 下可配置快捷键

### ssh配置免密码远程登陆
ssh-copy-id将本地公钥copy到远程服务器允许的主机中去
```
$ ssh-copy-id -i ~/.ssh/id_rsa.pub root@47.52.96.235
/usr/bin/ssh-copy-id: INFO: Source of key(s) to be installed: "/Users/Shiming/.ssh/id_rsa.pub"
The authenticity of host '47.52.96.235 (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:H0LIGfcGjxFjilR+V6IQt/T97MGRczTQvmx2jXE3Irs.
Are you sure you want to continue connecting (yes/no)? yes
/usr/bin/ssh-copy-id: INFO: attempting to log in with the new key(s), to filter out any that are already installed
/usr/bin/ssh-copy-id: INFO: 1 key(s) remain to be installed -- if you are prompted now it is to install the new keys
root@47.52.96.235's password: 

Number of key(s) added:        1

Now try logging into the machine, with:   "ssh 'root@47.52.96.235'"
and check to make sure that only the key(s) you wanted were added.
```

### ssh保持连接
ssh远程连接服务器老是超时自动断开，如何保持不断？
**方案一：在客户端设置**
方法很简单，只需在客户端电脑上编辑（需要root权限）/etc/ssh/ssh_config，并添加如下一行：

> ServerAliveInterval 30
 
此后该系统里的用户连接SSH时，每30秒会发一个KeepAlive请求，避免被踢。

**方案二：在服务器设置**
如果有相应的权限，也可以在服务器端设置，即编辑/etc/ssh/sshd_config，并添加：

> ClientAliveInterval 60

重启SSH服务器后该项设置会生效。每一个连接到此服务器上的客户端都会受其影响。应注意启用该功能后，安全性会有一定下降（比如忘记登出时……）

### mac中命令行调用起vscode打开目录/文件
https://code.visualstudio.com/docs/setup/mac

### 开机启动服务
Ubuntu开机之后会执行/etc/rc.local文件中的脚本，可以直接在/etc/rc.local中添加启动脚本, 要添加到语句：exit 0 前面才行。
``` bash
sudo vi /etc/rc.local
``` 

rc.local文件：
``` bash
#!/bin/sh -e
#
# rc.local
#
# This script is executed at the end of each multiuser runlevel.
# Make sure that the script will "exit 0" on success or any other
# value on error.
#
# In order to enable or disable this script just change the execution
# bits.
#
# By default this script does nothing.

# add by shiming to auto run in system restart for bitcoin testnet and ethereum testnet
nohup geth --testnet --datadir /mnt/ethereum/ --syncmode "full" --rpc --ws &
nohup btcd --testnet --datadir /mnt/bitcoin/ &
exit 0
```

### 使用nginx反向代理本地端口
nginx 的配置文件位置为 `/etc/nginx/nginx.conf`
但是在这个配置中include了其他配置文件
``` bash
        include /etc/nginx/conf.d/*.conf;
        include /etc/nginx/sites-enabled/*;
```
        
所以我们在conf.d中编写配置文件即可 `/etc/nginx/conf.d/btcd.conf`

``` bash
server{
        listen 9000;   # 对外端口
        # using web1 sub domain to access
        server_name 127.0.0.1 47.75.70.201;
        access_log  /var/log/nginx/btcd.log;

        location / {
            proxy_pass http://127.0.0.1:18334; # 代理端口
            proxy_read_timeout 300;
            proxy_connect_timeout 300;
            proxy_redirect     off;

            proxy_set_header   X-Forwarded-Proto $scheme;
            proxy_set_header   Host              $http_host;
            proxy_set_header   X-Real-IP         $remote_addr;
        }
    }
```  

配置完了检查nginx配置是否正确
``` bash
$ conf.d nginx -t
nginx: the configuration file /etc/nginx/nginx.conf syntax is ok
nginx: configuration file /etc/nginx/nginx.conf test is successful
```

重启nginx生效配置
``` bash
➜  conf.d systemctl restart nginx
```

查看端口是否被监听
``` bash
➜  conf.d lsof -i:9000
COMMAND  PID     USER   FD   TYPE DEVICE SIZE/OFF NODE NAME
nginx   2821     root    7u  IPv4 535089      0t0  TCP *:9000 (LISTEN)
nginx   2822 www-data    7u  IPv4 535089      0t0  TCP *:9000 (LISTEN)
nginx   2823 www-data    7u  IPv4 535089      0t0  TCP *:9000 (LISTEN)
nginx   2824 www-data    7u  IPv4 535089      0t0  TCP *:9000 (LISTEN)
nginx   2825 www-data    7u  IPv4 535089      0t0  TCP *:9000 (LISTEN)
nginx   2826 www-data    7u  IPv4 535089      0t0  TCP *:9000 (LISTEN)
nginx   2827 www-data    7u  IPv4 535089      0t0  TCP *:9000 (LISTEN)
nginx   2828 www-data    7u  IPv4 535089      0t0  TCP *:9000 (LISTEN)
nginx   2830 www-data    7u  IPv4 535089      0t0  TCP *:9000 (LISTEN)
```


### 在命令行中调用sublime text编辑文本
执行以下命令
``` bash
ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/sublime
```
参考 https://olivierlacan.com/posts/launch-sublime-text-3-from-the-command-line/

## troubleshooting
### -bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
centos ssh登录，登录成功但是报 -bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
```
➜  ~ ssh shiming@10.211.55.13
shiming@10.211.55.13's password:
Last login: Sat Oct 13 19:33:34 2018
-bash: warning: setlocale: LC_CTYPE: cannot change locale (UTF-8): No such file or directory
[shiming@centos ~]$
```
解决方案：
``` bash
sudo vi /etc/environment
```
然后加上这两行，再次登录就不会报了：
```
LANG=en_US.utf-8
LC_ALL=en_US.utf-8
```

### ssh connection refused
1. 先判断ssh是否安装
``` bash
shiming@ubuntu:/etc/ssh$ ps -e | grep ssh
shiming@ubuntu:/etc/ssh$ /etc/init.d/ssh -start
bash: /etc/init.d/ssh: No such file or directory
shiming@ubuntu:/etc/ssh$ whichis ssh
whichis: command not found
```
发现ssh未安装

2. 安装ssh-server
``` bash
shiming@ubuntu:/etc/ssh$ sudo apt-get install openssh-server
```
3. 启动ssh服务
``` bash
shiming@ubuntu:/etc/ssh$ systemctl start sshd
shiming@ubuntu:/etc/ssh$ ps -e|grep ssh
 5602 ?        00:00:00 sshd
```

4. 本地连接ssh进行测试
``` bash
shiming@ubuntu:/etc/ssh$ ssh shiming@localhost
The authenticity of host 'localhost (127.0.0.1)' can't be established.
ECDSA key fingerprint is SHA256:fHN3yPgM87SlGdXxzvvCGzqf3ARmN2iyyq9EfNwSMo4.
Are you sure you want to continue connecting (yes/no)? yes
Warning: Permanently added 'localhost' (ECDSA) to the list of known hosts.
shiming@localhost's password: 
Welcome to Ubuntu 16.04.3 LTS (GNU/Linux 4.10.0-28-generic x86_64)
```

5. ifconfig查看外网地址
inet即外网地址
``` bash
shiming@ubuntu:/etc/ssh$ ifconfig
enp0s5    Link encap:Ethernet  HWaddr 00:1c:42:28:80:a2  
          inet addr:10.211.55.7  Bcast:10.211.55.255  Mask:255.255.255.0
          inet6 addr: fe80::2598:3ddc:aea:479b/64 Scope:Link
          inet6 addr: fdb2:2c26:f4e4:0:2cb3:821a:c4:a047/64 Scope:Global
          inet6 addr: fdb2:2c26:f4e4:0:2991:5c69:98eb:d6a5/64 Scope:Global
          UP BROADCAST RUNNING MULTICAST  MTU:1500  Metric:1
          RX packets:1142 errors:0 dropped:0 overruns:0 frame:0
          TX packets:840 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:1332342 (1.3 MB)  TX bytes:83530 (83.5 KB)

lo        Link encap:Local Loopback  
          inet addr:127.0.0.1  Mask:255.0.0.0
          inet6 addr: ::1/128 Scope:Host
          UP LOOPBACK RUNNING  MTU:65536  Metric:1
          RX packets:310 errors:0 dropped:0 overruns:0 frame:0
          TX packets:310 errors:0 dropped:0 overruns:0 carrier:0
          collisions:0 txqueuelen:1000 
          RX bytes:27329 (27.3 KB)  TX bytes:27329 (27.3 KB)
```

6. 通过外网进行ssh连接（略）

### vi编辑，上下左右箭头变成ABCD/delete键无法删除解决办法
https://askubuntu.com/questions/353911/hitting-arrow-keys-adds-characters-in-vi-editor

### 关闭ubuntu图形界面
关闭图形界面可以让虚拟机少占用一些资源
参考： https://wiki.zthxxx.me/wiki/%E6%8A%80%E6%9C%AF%E5%BC%80%E5%8F%91/Linux/Ubuntu/Ubuntu-16-%E5%BC%80%E6%9C%BA%E9%BB%98%E8%AE%A4%E5%91%BD%E4%BB%A4%E8%A1%8C%E7%95%8C%E9%9D%A2/
``` bash
shiming@ubuntu:~$ sudo systemctl set-default multi-user.target
[sudo] password for shiming: 
Created symlink from /etc/systemd/system/default.target to /lib/systemd/system/multi-user.target.
```

### 关闭centos图形界面
``` bash
➜  ~ systemctl set-default multi-user.target
Removed symlink /etc/systemd/system/default.target.
Created symlink from /etc/systemd/system/default.target to /usr/lib/systemd/system/multi-user.target.
```
### 显示当前主机的信息
``` bash
$ hostnamectl
```

### 修改hostname
``` bash
hostnamectl set-hostname newhostnameyouwant
```

### 将远程服务器的文件复制到本地剪贴板
``` bash
ssh -e none root@47.75.70.201 "cat /tmp/bb.conf" | pbcopy  #到本地剪贴板
pbpaste > /tmp/bb.txt #本地剪贴板到本地文件
```

### 升级vim
https://stackoverflow.com/questions/39861793/how-update-vim-to-8-0-version-in-osx

### 安装vim-go




## reference

### bash reference
http://www.gnu.org/software/bash/manual/bashref.html








