# centos 常见问题

## 驱动问题

[解决方案](https://blog.csdn.net/gatieme/article/details/71075394)
CentOS下支持挂载exFAT与NTFS文件系统

### exFAT

#### 安装依赖

下载源 [rpmfusion-free-release-7.noarch.rpm](download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm)

```linux
sudo yum install fuse-exfat
sudo yum install exfat-utils
```

#### 挂载

```linux
sudo mount.exfat /dev/sdc1 /mnt
OR
sudo mount /dev/sdc1 /mnt
```

### NTFS系统

#### 安装依赖

`ntfs-3g`

##### yum安装

请确定你已经安装了 `rpmforge` 软件库的源. 下载源 [rpmfusion-free-release-7.noarch.rpm](download1.rpmfusion.org/free/el/rpmfusion-free-release-7.noarch.rpm)

```yum install fuse ntfs-3g -y
```

#### 挂载NTFS文件系统

```linux
mkdir /mnt/windows/c

mount -t ntfs-3g /dev/sdb1 /mnt/windows/c
OR
mount /dev/sdb1 /mnt/windows/c
```

### 挂载后访问ntfs系统只读问题

[解决方案](https://zhuanlan.zhihu.com/p/161505413)

```linux
sudo umount /mnt/win10
sudo ntfs-3g -o remove_hiberfile /dev/sda1 /mnt/win10
```

发现原本按教程走而创建的`/mnt/windows/c`，理应挂载点在`/mnt/windows/c`，但现在不知道挂载点具体哪个位置，怎么`umount`

#### 查看挂载点

df 选项 文件目录或文件名
参数：
-a. --all ,显示所有的文件系统，包括虚拟文件系统
-B。--block-size 指定单位大小，比如1K，1M等
-h，--human-readable 以人们易读的GB，MB，KB等格式显示
-H。--si和-h参数一样，但不是一1024，而是1000，即1K=1000，而不是1K=1024
-i，--inodes，不用硬盘容量，而是以inode的数量来显示
-k，以KB的容量显示各文件系统，相当于--block-size=1k
-m，以MB的容量显示各文件系统，相当于--block-size=1m
-l，--local，只显示本地文件系统
--no-sync； 在统计使用信息之前不调用sync命令
-sync，在统计使用信息之前调用snyc命令
-P，portability，使用POSIX格式显示
-t，--type=TYPE，只显示指定类型的文件系统
-T，--print-type，显示文件系统类型
-x,--exclude-type=TYPE ,不显示指定类型的文件系统
--help，显示帮助信息
--version。显示版本信息
[如何查看](https://blog.csdn.net/cym_anhui/article/details/80567996)

#### 没有解决

挂载点在 `/run/media/root/work`，似乎是自动地

#### 解决方案二

方式1：umount /dev/sda1

mount /dev/sda1 /boot

如果发现有提示“device is busy”，找到是什么进程使得他busy

fuser -m /boot 将会显示使用这个模块的pid

fuser -mk /boot 将会直接kill那个pid

然后重新mount即可。

* * *

 方式2：直接remount，命令为 u

[root@localhost ~]# mount -o rw,remount /boot

或者mount -o remount,rw /boot

**结果：能添加文件，但重启后linux端保存在ntfs系统上的文件全消失；**
> 放弃挂载新硬盘在Centos上
* * *

## Centos 安装LATEX

## Centos 设置软件快捷键在桌面上

```sell
[Desktop Entry]

Version=2021.1.3

Type=Application

Name=IDEA
##桌面图标名称

Comment=Sophisticated text editor for code, markup and prose

Exec=/opt/ideaIU-2021.1.3/idea-IU-211.7628.21/bin/idea.sh
 ##执行文件的位置，这里替换成你自己的

Terminal=false

Icon=/opt/ideaIU-2021.1.3/idea-IU-211.7628.21/bin/idea.png
 ##图标的位置，修改成你自己的

Categories=Development;               
```

## 安装JAVA

1. **卸载老版本**

* `rpm -qa | grep java`

* `rpm -qa | grep jdk`

* `rpm -qa | grep gcj`

* `rpm -e --nodeps java--1.8.*`

2. **下载**

[官网下载jdk-16.0.1_linux-x64_bin.tar.gz](https://www.oracle.com/java/technologies/javase-jdk16-downloads.html)


3. 解压

`tar -zxvf jdk-16.0.1_linux-x64_bin.tar.gz -C /opt`

4. 配置

```shell
#java
JAVA_HOME=/opt/jdk-16.0.1
JRE_HOME=$JAVA_HOME/jre
CLASSPATH=.:$JAVA_HOME/jre/lib/rt.jar:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar
PATH=$PATH:$JAVA_HOME/bin:$JRE_HOME/bin
export JAVA_HOME
export JRE_HOME
export PATH
export CLASSPATH
```
