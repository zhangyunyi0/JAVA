## Linux基本操作命令总结
### 1、命令基本格式
root用户：[root@localhost~]#或者普通用户：[hadoop@localhost~]$

用户@主机名 目录[#|$]管理员类型

root用户家目录：/root

普通用户家目录(比如hadoop)：/home/hadoop

pwd显示当前所在位置

一般命令格式：命令[选项][参数]参数可以是完全也可以是简化，比如：-a和--all

查看目录信息：ls ls -l ls -l dir等大小单位为B，如果要显示更容易识别大小：ls -lh, ls -i列出文件的id号，系统就是通过id识别文件

文件权限：-rwxr-xr--，第一个是文件类型：-代表文件 d代表目录 l代表软链接

Linux的7种文件类型：普通文件、目录文件、链接文件、块设备文件、字符设备文件、套接字文件、管道文件

### 2、目录文件处理
建立目录：mkdir 比如：mkdir abc

递归建立目录：mkdir -p 比如：mkdir -p abc/abc

切换当前目录：cd比如：cd /home/abc

进入家目录：cd ~或cd 

进入上一层目录：cd ..或者上上层：cd ../../

进入上一次所在的目录cd -

TAB键自动补全

打印当前目录：pwd

删除文件：rm filename比如rm abc

删除文件避免提示：rm -f abc

递归删除整个目录：rm -rf dir 比如rm -rf /tmp/* 删除tmp目录下所有的文件（包括目录）如果不加*表示直接删除tmp目录

删除空目录：rmdir dirname

复制文件并改名：cp abc /tmp/abcs 不改名：cp abc /tmp/

复制整个目录:cp -r /tmp/

为了保持文件修改时间等所有属性一致使用：cp -a 源目录 目标目录相当于cp -pdr 源目录 目标目录 r递归 p连带文件属性 d如果是链接文件，则复制链接文件属性

ls -l和ll等同

移动文件：mv 源文件或目录 目标文件或目录 复制目录和文件都一样不用加参数 源文件和目标文件在同一目录下直接用mv实现重命名

/bin /sbin /usr/bin /usr/sbin都是保存命令的 其中/sbin和/usr/sbin只有root用户能操作

/dev 硬件设备，挂载使用

/etc 配置常用

/home和/root是用户家目录

/lib系统库

/media和/mnt和/misc用来挂载外接存储设备，基本上都是用/mnt下创建新目录进行挂载

/proc和/sys是存放内存实时数据，不要随便操作

/tmp 临时数据存放目录

/usr 软件安装目录如/usr/java下面存放相应的包等

/var 软件安装对应配置或者文档等

链接命令：ln

硬链接-占有硬盘块：和源文件在的文件索引表数据存储空间完全一致，inode一致，都是访问同一个存储空间，只是两个不同位置，实质上就是同一个文件，如果删除一个文件，存储空间不会被释放，另外一个文件仍然可以正常访问，都删除则释放，相当于指针或者前后门，硬链接不能跨分区创建，因为跨分区无法访问同一个存储空间，只能是同一分区之下的普通文件，不能是目录。硬链接使用会导致多入口混乱，并且限制较大，所以推荐使用软链接

硬链接创建：ln 源文件 目标路径（目标路径文件名必须写全）

软链接，类似于Windows下的快捷方式，软链接拥有自己的inode和存储空间，只是保存目标文件的属性信息，包括inode节点，位置等等，修改软链接其实就是修改原始文件，删除源文件软链接失效，删除软链接源文件也同样删除

软链接创建（注意必须使用绝对路径，否则保存相对目录会导致出错）：ls -s [源文件(目录)]/home/hadooptest/app/abcd[目标软链接]/tmp/test.soft

### 3、文件搜索

搜索文件名：locate 文件名 原理：从数据库索引中进行搜索，支持模糊查询

/var/lib/mlocate是locate的数据库

更新locate数据库（默认一天一更新，避免搜索不到新建文件）：updatedb

locate搜索的配置文件/etc/updatedb.conf配置搜索的筛选规则

搜索命令：whereis 命令名

比如：whereis ls能够列出命令对应的程序位置，帮助文档位置；加-b只查看源程序位置，-m只查看帮助文档位置

搜索命令：whatis 命令名，什么作用

比如：whatis ls列出ls命令是做什么的

搜索命令：which 命令名

比如：which ls能够列出在什么位置，并且列出高亮的一些参数选项比如ls --colr=auto等并且如果命令没有这些选择只显示位置，不显示其他，cd命令没有位置，cd命令是shell环境自带的，或者说是kernel自带的核心命令

自己开发或者定义的命令系统环境下的命令（/bin,/sbin,/usr/bin,/usr/sbin这些系统默认执行环境）或者放在环境变量下无法被查找到

最强大的搜索命令：find命令

按文件名搜索：find/-name test.log最好不要指定根目录，否则会很慢，按文件名搜索是完全匹配，可以使用通配符，常用的有\* ? [],比如find /tmp -name "\*.log"最好加引号匹配字符串表达式

搜索没有用户所有的文件：find / -nouser包括垃圾文件，外来文件，内核产生的文件

按照所属用户搜索文件：find /home -user root

按时间搜索：find /var/log -mtime+10查找10天前文件内容被修改的文件，-atime文件访问时间，-ctime文件属性被修改，-10代表10天内被响应操作的文件，10代表第10天前当天被修改的文件

按照文件大小来搜索：find /home/hadooptest/ -size 25k搜索大小为25k的文件，-25k是小于25k，+25k是大于25k，这里的k必须小写，按M搜索必须是大写，按字节大小是b必须小写，一般要加单位，如果不加单位代表硬盘数据块块数而并不是B比较难计算

按照文件inode节点来搜索：find /home -inum 26262

逻辑与查询用-a比如find /home -size +20k -a -size -50k表示查找大于20k并且小于50k的文件

逻辑或查询用-o使用一样

查找并显示详细信息：find /home -size +20k -a -size -50k -exec ls -lh{}\;

-exec是代表调用命令，{}\;是固定格式，之间是第二条命令，表示将前面命令的输出结果交给后面的命令继续执行，要保持执行才可以，比如：find /tmp -nouser -exec rm -rf{}\;查找并删除

字符串搜索：grep

搜索文件中包含指定关键字的行，比如：grep "size" abc.cfg在abc.cfg文件查找包括"size"关键字的行并且列出

参数-v是排除关键字，-i是忽略大小写比如grep -v "define" config.h

find可以和grep一起使用，find是文件名匹配，完全匹配（可以使用通配符匹配）；grep是文本内容搜索，包含匹配（使用正则表达式匹配）

### 4、命令帮助

查看命令帮助，比如：man ls可以通过翻页，上下键、回车往下循环滚动，按q键退出

想查看某个参数就在帮助页输入/然后输入参数比如-q回车，然后可以查找-q参数的使用方法，按n可以按照顺序依次跳转多个选项

man分为9个级别

man ls是查看默认级别

man -f ls查看ls存在几个级别相当于whatis ls

通过man 1 ls查看指定等级的帮助

man -k password或者apropos passwd查看和passwd所有相关的命令，如果记不太清可以查找另外的帮助，比如：ls --help目前shell终端支持中文帮助

获取内部命令帮助help cd，首先用whereis cd查看是否是内部命令，然后使用help内部命令来获取帮助，内部命令不能用--help或者man来帮助

info ls查看更详细的文档，比man还要详细，会显示多种版本的详细文档

info显示页面使用u进入上一层，n进入下一个小节，p进入上一个小节，q退出

### 5、文件压缩归档操作

常用压缩格式：.zip .gz bz2 .tgz .tar.gz .tar.bz .tar.bz2等

压缩文件成zip：zip abc.zip abc.txt

压缩目录成zip：zip -r abc.zip ./abc/

解压缩zip：unzip abc.zip

压缩文件成gz：gzip abc.txt不用加压缩的文件名，自动分配源文件名后加.gz，压缩之后源文件会删除

自定义压缩并且不删除源文件：gzip -c 源文件>压缩文件（不建议这样使用-c是输出压缩编码，采用重定向的技巧实现，并不是专用）

压缩目录：gzip -r 目录，这样并不会打包，而是把目录下的每个文件都递归压缩一遍

解压缩文件：gzip -d abc.gz或者gunzip abc.gz都可以解压缩，解压缩后也会删除原包

bz2格式压缩：bzip2 源文件，不会保留源文件

bzip2 -k 源文件，压缩之后保留源文件

bzip2不能压缩目录

解压缩bz2格式：bzip2 -d 压缩包或者bunzip2 压缩包，两个目录默认都不保留压缩包，加-k都可以保留

tar打包：tar -cvf，打包文件名、源文件或目录	，-c打包 -v显示详细信息 -f指定打包后的文件名

例如：tar -cvf abc.tar ./abc/

打包之后可以使用bzip2或者gzip进行压缩

tar解包：tar -xvf abc.tar	，-x是释放归档

.tar.gz一并完成(.tgz通用)：

打包：tar -zcvf abc.tar.gz abc/

解包：tar -zxvf abc.tar.gz

指定目录：tar -zxvf abc.tar.gz -C /home/app

只查看不压缩用：tar -ztvf abc.tar.gz

.tar.bz2一并完成：

打包：tar -jcvf abc.tar.bz2 abc/

解包：tar -jxvf abc.tar.bz2

指定目录用：tar -jxvf abc.tar.bz2 -C /tmp/

只查看不压缩用：tar -jtvf abc.tar.bz2

### 6、关机和重启命令（关机重启是自动优雅结束服务，比较建议）

10分钟后重启：shutdown -r 10

10分钟后关机：shutdown -h 10

定时重启：shutdown -r 05:30 &

定时关机：shutdown -h 05:30 &

取消定时命令：shutdown -c

立即重启：shutdown -r now或者shutdown -r 0

立即关机：shutdown -h now或者shutdown -h 0

服务器因为是远程控制，所以建议只进行重启，不进行关机

服务器运行过程中，一定要正确的关闭服务，保存相应的数据，有序重启，启动后，有序的操作各种服务

其他关机命令：poweroff、half、init 0不建议使用，会造成不正常结束

其他重启命令：reboot（相对来说比较安全）、init 6（不建议使用）

init 运行级别分为7个，调用相应的级别进行相应的操作

init 0 关机

init 1 单用户（相当于Windows安全模式，纯命令行界面最小服务）
  
init 2 不完全多用户，不含NFS服务（命令行）

init 3 完全多用户（一般使用的方式）

init 4 未分配

init 5 图形界面

init 6 重启

runlevel查看当前系统运行级别

系统默认运行级别保存在：/etc/inittab最后一行指定默认启动级别

退出当前登录用户（Linux一般允许同时登陆256个，Windows XP只允许1个用户、后来的允许2-8个之间：logout

远程ssh shell管理一定要正确退出用户，否则直接关闭窗口会占用并发，用户并未退出，影响服务器性能

注销用户：logout

退出shell：exit，一般返回状态码0之后也会注销用户，建议使用logout注销

### 7、挂载命令

mount查看当前挂载的对应设备

mount -a根据配置文件/etc/fstab的内容自动挂载

尽量不要自动挂载光盘或者U盘，如果忘记插入设备，系统将无法启动，建议只挂载系统分区

挂载设备：mount [-t 文件系统] [-o 特殊选项] 设备文件名 挂载点

Linux默认支持ext3、ext4文件系统，光盘文件系统为iso9660

重新挂载分区的同时制定特殊选项，比如：mount -o remount,noexec /home/表示重新挂载home分区，并且不允许可执行文件执行

测试完一定要尽快改回去，避免提示权限不足的异常错觉：mount -o remount,exec /home/

### 8、用户登录查看

w查看当前系统运行的时间和已经登录的用户信息，包括终端、登录来源IP、时间等信息

who和w差不多，也是显示登录用户的所有信息，内容比w少一些，更精简

last查看服务器所有用户的登录记录信息等，包括系统重启时间；可以检测异常登录

last命令对应文件存在于/var/log/wtmp下，wtmp是二进制文件，不是文本文件，所以不能用编辑器修改，就是为了防止日志篡改，如果发现last命令异常，服务器可能入侵

lastlog查看所有用户最后一次登录信息，判断是否登陆过，也是存放在/var/log/wtmp



