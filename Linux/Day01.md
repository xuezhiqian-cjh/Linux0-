# Day01 Linux基础


## 今日学习
### 查看服务器配置信息cpu 内存磁盘
- 查看操作系统版本
```bash
cat /etc/os-release
```
- 查看cup情况
```bash
lscpu
# Caches (sum of all):      
#   L1d:                    96 KiB (2 instances)
#   L1i:                    64 KiB (2 instances)
#   L2:                     2.5 MiB (2 instances)
#   L3:                     24 MiB (1 instance)
#   缓存越大，效率越高
# CPU:                      2   （cpu核数越多，效率越高）

cat /proc/cpuinfo
# cpu MHz		: 2918.397  (cpu主频，越大越快)
```
- 查看服务器运行内存
```bash
free
# [root@localhost ~]# free
#                total        used        free      shared  buff/cache   available
# Mem:         3453448      636560     2649960        9292      393192     2816888
# Swap:        4112380           0     4112380

# swap是虚拟内存，物理内存不够用的时候才会使用这个，没有虚拟内存，设备也可以正常运行，但是磁盘和内存消耗很大时，可能卡住
```

- 查看磁盘
```bash
lsblk
df -h
# 挂载点：分区的门。访问挂载点就等于访问文件系统

lspci
#查看主板上的一些硬件信息，通常配合管道符 | 使用grep ***

lsusb
#查看cpu接口

uname -r 
#查看内核
# [root@localhost ~]# uname -r
# 6.6.0-132.0.0.111.oe2403sp3.x86_64
 # 第一个6： 主版本号
 # 第二个6： 次版本号，偶数说明是稳定版，奇数就是开发或测试版（不稳定）
 #  0-132： 末版本号 ，更新会随着系统改变

uname -n
# 查看主机名
```

### 服务器时钟
```bash
# 一定要打开ntp服务，查看是否打开ntp：
timedatectl

timedatectl set-ntp BOOL
timedatectl set-time "2026-05-06 14:05:55"
timedatectl set-local-rtc BOOL
timedatectl --help就行
timedatectl list-timezones
```

### hostnamectl主机名设置
```bash
hostnamectl --static set-hostname www.cjh.com

-   **`Static hostname` (静态主机名)**：是服务器的**法定身份证**，系统启动时用它。
-   **`Pretty hostname` (美化主机名)**：是服务器的**昵称**，给人看的。
-   **`Transient hostname` (临时主机名)**：是服务器的**临时外号**，由网络环境动态分配。


远程操作主机名
hostnamectl -H root@192.168.66.66 status
hostnamectl -H root@192.168.66.66 set-location xxxxxx
hostnamectl -H root@192.168.66.66 set-hostname www.ccc.com
```


### 时间戳
```bash
[root@localhost ~]# date +%s
1784532098
[root@localhost ~]# date -d "@1784532098"
2026年 07月 20日 星期一 15:21:38 CST
```




