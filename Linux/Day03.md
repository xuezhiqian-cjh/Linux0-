# Day3
### bash历史记录

- `history`会显示以前执行过的1000个命令,并且保存在当前路径下的`.bash_history`

- 问：如何让history显示命令执行的时间？
  答：定义了 `HISTTIMEFORMAT`之后就会显示时间。如下：
```bash
[root@cjh ~]# export HISTTIMEFORMAT="%F %T `whoami` "
# HISTTIMEFORMAT是一个内置的特殊的环境变量
# %F、%T是完整的日期和时间
# whoami是谁执行的命令


[root@cjh ~]# echo $HISTTIMEFORMAT
%F %T root
# 验证一下是否写进去变量了


[root@cjh ~]# history | head
    1  2026-07-21 08:50:23 root ip a
    2  2026-07-21 08:50:23 root vim /etc/ssh/sshd_config 
    3  2026-07-21 08:50:23 root vi /etc/ssh/sshd_config 


# 只执行export是临时的，只有echo写入文件中才会永久存在
echo export HISTTIMEFORMAT="\'%F %T \`whoami\` \" >> /etc/profile
# \和c语言一样都是转义字符配套使用的
# /etc/profile是所有用户（全局配置文件）
# ~/.bashrc是当前用户


# 清楚所有历史记录
history -c     # 但是文件中还有历史记录，没有彻底清楚
rm -rf .bash_history    # 删掉这个文件才会彻底清楚历史记录


```

- 使用 `!`+`history出来的命令序号`就可以直接执行对应的命令
- `crtl`+`r`可以快捷搜索执行过的命令



### 字符集中英文切换

！ 切换字符集主要是为了解决乱码问题
```bash
# 查看是什么语言
cat /etc/locale.conf
[root@cjh ~]# localectl 
System Locale: LANG=zh_CN.UTF-8
    VC Keymap: cn
   X11 Layout: cn


# 查看有什么字符集
[root@cjh ~]# localectl list-locales 
C.UTF-8
en_AG.UTF-8
en_AU.UTF-8
en_BW.UTF-8
en_CA.UTF-8
en_DK.UTF-8
....


# 设置字符集
localectl set-locale LANG=en_AG.UTF-8

# 重新加载资源，即可立即切换字符集
source /etc/locale.conf
```

### alias定义或显示命令别名
- 感觉和c语言的typedef挺像
```bash
# 临时修改     alias 新命令='原命令'
[root@cjh ~]# alias lo='ls -alh'


# 永久修改，写入文件
[root@cjh ~]# echo "alias lo='ls -alh'" >> ~/.bashrc
# 都是在bashrc文件中
```

```bash
# 例如：避免删除某文件，就会用到这个确认是否删除
也就是： rm = rm -i

反正就是简化命令等作用
```
