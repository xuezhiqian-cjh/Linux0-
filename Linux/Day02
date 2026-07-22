### ln符号链接和硬链接和l节点的作用
```bash
# 1. 创建测试文件
echo "Hello World" > test.txt

# 2. 创建软链接和硬链接
ln -s test.txt soft_link   # 软链接
ln test.txt hard_link      # 硬链接

# 3. 查看 inode 号 (关键！看数字是否一样)
ls -i test.txt soft_link hard_link

# 4. 删除源文件，观察现象
rm test.txt
cat soft_link    # 报错：No such file or directory
cat hard_link    # 依然显示：Hello World
```

### split大文件切割和合并
```bash
split -l passwd
du -sh passwd
ll -h passwd
--help就可以都查出来
```

### `diff`文件差异对比和补丁管理
```bash
# 比较文件和目录内容
diff --help查看内容吧
diff f1 f2
[root@www ~]# diff f1 f2
4c4
< a
---
> b

# 合并文件上下文
[root@www ~]# diff -u f1 f2
--- f1	2026-07-20 21:06:04.693379818 +0800
+++ f2	2026-07-20 21:06:54.262939128 +0800
@@ -1,7 +1,7 @@
 a
 a
 a
-a
+b
 a
 a
 a
```

- 补丁
```bash
[root@www ~]# diff -e f1 f2 > ab.txt
# 把f1 f2 的差异写道ab.txt中
[root@www ~]# cat ab.txt 
4c
b
.

[root@www ~]# echo "w" >> ab.txt 
# 把w功能追加进去
[root@www ~]# cat ab.txt 
4c
b
.
w


[root@www ~]# ed - f1 < ab.txt 
# 利用ed命令同步f1 f2内容
[root@www ~]# cat f1
a
a
a
b
a
a
a
```

- 差异同步  
```bash
rsync -a -v -z --delete dir2/ dir1/
# 以dir2为标准，精准同步dir1的所有内容
```



- 详解补丁的生成path，打补丁与撤销补丁
```bash
# 生成补丁
diff -uNr dir1 dir2 > dir.patch
[root@cjh ~]# diff -uNr dir1 dir2 > dir.patch
[root@cjh ~]# cat dir.patch 
diff -uNr dir1/test1.txt dir2/test1.txt
--- dir1/test1.txt	2026-07-21 08:43:06.012231240 +0800
+++ dir2/test1.txt	2026-07-21 08:48:07.746195373 +0800
@@ -1 +1 @@
-c7.com
+c7.com1111111
diff -uNr dir1/test2.txt dir2/test2.txt
--- dir1/test2.txt	2026-07-21 08:43:31.654423299 +0800
+++ dir2/test2.txt	2026-07-21 08:48:20.325711158 +0800
@@ -1 +1 @@
-hahahah
+hahahahbbbbbbb

# 修补目录    ！！先进入要修补的目录中
[root@cjh dir1]# patch -p1 < /root/dir.patch 
patching file test1.txt
patching file test2.txt
[root@cjh dir1]# cat test1.txt 
c7.com1111111
[root@cjh dir1]# cat test2.txt 
hahahahbbbbbbb

# p0、1、2：就好比拆快递时候扔掉几层包装。比如系统看到补丁写的是 `my_blog/app.py`，因为-p0不扔包装，所以就去找 `my_blog`文件夹，然后再去找 `app.py` .-p1就是忽略 `my_blog`直接在当前目录下找 `app.py`

# 撤销补丁    加了一个-R
[root@cjh dir1]# patch -R -p1 < /root/dir.patch 
patching file test1.txt
patching file test2.txt
[root@cjh dir1]# cat test1.txt 
c7.com

```
