---
title: Linux基本命令
date: 2022-08-03 22:36
---





# 连接服务器

服务器通过ssh协议进行链接，确保电脑装有ssh客户端，然后使用以下命令链接服务器：

 ```
 ssh user@remote_ip                                                  
 ```



# 命令


## 常用命令

1. 自动补全： `Tab` 能够自动补全参数，在需要输入命名或者文件名时候十分有效。

2. ls 列举当前目录下文件名，后面跟路径能列举指定文件夹下文件
   ```
   -a  ：全部的文件，连同隐藏文件（ 开头为 . 的文件） 一起列出来（常用）
   -l  ：长数据串行出，包含文件的属性与权限等等数据；（常用）
   -A  ：全部的文件，连同隐藏文件，但不包括 . 与 .. 这两个目录
   -d  ：仅列出目录本身，而不是列出目录内的文件数据（常用）
   -h  ：将文件大小以人类较易读的方式（例如 GB, KB 等等）列出来；
   ...
   ```

   

3. `cd` 切换工作路径，`cd ~` 返回自己的home路径，`cd -` 返回上一个工作路径。

4. `nohup` 可以在退出终端后继续运行进程。默认情况下进程的作业打印输出被重定向存放在nohup.out文件中。

5. 如果想要将程序放到后台执行，在该命令后面加上`&`

6. `ctrl + c` 强制终端结束进程。
   `ctrl + z`  暂停进程。 `fg`命令重新启动前台被中断的任务,`bg`命令把被中断的任务放在后台执行.

   `jobs` 显示当前暂停的任务。

   `fg N` ` 或者 %N` 将第N个任务在前台运行，`bg N` 将第N个任务放在后台运行。`bg`，`fg`不带N时表示对最后一个进程操作

7. pwd查看当前工作路径

8. 

### 特殊目录

| 符号       | 意义                                  |
| ---------- | ------------------------------------- |
| `.`        | 当前工作目录                          |
| `..`       | 上一级目录                            |
| `-`        | 上一个工作目录                        |
| `~`        | 当前用户主文件夹，即`/home/userName/` |
| `-account` | account用户的主文件夹                 |
| `/`        | 根目录                                |

 





## 有用的命令

1. 查看历史命令： `history` 能够查看以前输入的命令。使用`!n` （n是该命令的序号）执行该命令; `!$` 表示上一个命令后面参数，`!!` 指代上一个命令(当然用`上键`也可以直接调出上一个命令)。

2. 搜索历史记录： `ctrl + r` 能够向前检索历史命名，输入关键词即可显示最近的命令记录。回车即执行命令。

3. `ctrl + w` 删除光标前的最后一个单词；`ctrl + u`删除光标前的所有内容；ctrl + k删除光标后的所有内容
   `ctrl + b`  可以向前移动一个字符位置，与`左键`同效果；`ctrl + f ` 向后前移动，与` 右键`同效果

   `alt + b`  可以向前移动一个单词位置；`alt + f ` 向后前一个单词位置移动

   `ctrl + a` 移动到行首，`ctrl+ e` 移动到行尾

4. `clear` 清除屏幕，`ctrl + l`同样效果

5. 命令前面加上`#` 该命名将不会执行，但是会出现在history记录中，以方便以后查看。`alt + #` 快速将该行命令注释

6. `alias` 查看系统中的别名，也可以创建别名，例如`alias ll = 'ls -la'` 当输入命令`ll` 就相当于输入了`ls -la`

7. 使用重定向`>` 和`<` 可以将指定输出存放到文件，`>>`  用以追加文件。

8. `ln`  只能给文件创建硬链接
   `ln -s`  创建软连接，相当于Windows中的快捷方式

   ```shell
   ln [参数] [源文件或目录] [目标文件或目录]
   ln a.txt b.txt
   ```

   

 



# 文件操作
## 修改文件夹

* 使用`touch`创建一个空文件 

  ```shell
  touch file1.txt #创建一个文件
  touch file1.txt file2.txt file3.txt #创建多个文件
  ```
  
* 使用`mkdir`创建 文件夹

  ```shell
  mkdir [-p] dirName  #mkdir [-p] dirName
  ```


* 删除文件/删除文件夹

  `rm`用来删除文件或者目录

  ```
  -i 删除前逐一询问确认
  -f 强制删除，无需确认
  -r 将目录及以下之档案亦逐一删除
  ```

    例如

  ```shell
  rm test.txt #删除当前目录下test.txt文件
  rm -r test #删除当前目录下test文件夹
  ```

  **使用删除时候需要谨慎！**

* 查看文件内容/查看文件夹目录

  * 使用`ls`来查看文件夹下的文件
  * 使用`cat,more,less`来阅读文本文件

* 移动文件（夹）

  使用`mv` 来移动文件：

  ```bash
  mv [-fiu] source destination #将source移动到destination（desntination可以是目录若目录不存在，则以目录名为文件名）
  mv [options] source1 source2 source3 .... directory # 将多个文件移动到目录下
  选项与参数：
  -f  ：force 强制的意思，如果目标文件已经存在，不会询问而直接覆盖；
  -i  ：若目标文件 （destination） 已经存在时，就会询问是否覆盖！
  -u  ：若目标文件已经存在，且 source 比较新，才会更新 （update）
  ```

* 拷贝文件（夹）
  使用`cp` 来复制文件。

  **要能拷贝该文件，必须要有对该文件的读权限。**
  
  ```bash
  cp [-adfilprsu] 来源文件（source） 目标文件（destination）
  cp [options] source1 source2 source3 .... directory
  选项与参数：
  -a  ：相当于 -dr --preserve=all 的意思，至于 dr 请参考下列说明；（常用）
  -d  ：若来源文件为链接文件的属性（link file），则复制链接文件属性而非文件本身；
  -f  ：为强制（force）的意思，若目标文件已经存在且无法打开，则移除后再尝试一次；
  -i  ：若目标文件（destination）已经存在时，在覆盖时会先询问动作的进行（常用）
  -l  ：进行硬式链接（hard link）的链接文件创建，而非复制文件本身；
  -p  ：连同文件的属性（权限、用户、时间）一起复制过去，而非使用默认属性（备份常用）；
  -r  ：递回持续复制，用于目录的复制行为；（常用）
  -s  ：复制成为符号链接文件 （symbolic link），亦即“捷径”文件；
  -u  ：destination 比 source 旧才更新 destination，或 destination 不存在的情况下才复制。
  --preserve=all ：除了 -p 的权限相关参数外，还加入 SELinux 的属性, links, xattr 等也复制了。
  最后需要注意的，如果来源文件有两个以上，则最后一个目的文件一定要是“目录”才行！
  ```
  
* 文件（夹）重命名

  * 使用`mv` 将文件（夹）重新移动到当前工作位置实现重新命名

  * 批量重命名请查看`rename` 用法。

## 下载文件/上传文件

* 从网络下载文件
  ```
  wget URL
  ```
  通过`wget`下载链接的文件，它将下载到当前目录下，文件名为原始文件名。
  
* 将本地文件传到服务器
  scp 是 secure copy 的缩写, scp 是 linux 系统下**基于 ssh** 登陆进行安全的远程文件拷贝命令。

  在**本地终端**输入以下命令：

  ```shell
  #复制文件
  scp local_file remote_username@remote_ip:remote_file
  #例如
  scp /test.txt root@172.1.0.1:~/test # 将本地的test.txt文件放到服务器( 172.1.0.1 )root账号的home目录下( ~表示登录账号的home目录) 的test文件夹下，如果test文件夹不存在，则在~目录下改名为test文件。
  
  
  # 加入-r参数将本地文件夹复制到服务器
  scp -r local_folder remote_username@remote_ip:remote_file 
  ```
  
* 将服务器文件下载到本地
  
  将服务器位置和本地位置对调就可以从远程下载文件和文件夹了！
  
  ```
  scp remote_username@remote_ip:remote_file local_file 
  scp remote_username@remote_ip:remote_folder local_folder 
  ```
  
  
  
  
  
## 压缩文件/解压文件

| 压缩后缀 | 压缩方法                                            | 解压方法              |                      |
| -------- | --------------------------------------------------- | --------------------- | -------------------- |
| .zip     | zip压缩                                             | unzip filename.zip    |                      |
| .gz      | gzip  filename                                      | gzip -d filename.gz   | 压缩后会将原文件删除 |
| .bz2     | bzip2 filename<br />bzip2 -k filename(保留原始文件) | bzip2 -d finename.bz2 |                      |
| .xz      | xz filename<br/><br/>xz -k filename                 | xz -d  finename.xz    |                      |

使用`tar` 进行打包压缩或者解压：

```
tar [-j|-z] [cv] [-f ] filename... <==打包不压缩 
tar [-j|-z] [tv] [-f ]             <==察看檔名 
tar [-j|-z] [xv] [-f] [-C 目录]     <==解压缩 
选顷不参数:
					-c  :压缩
					-t  :查看
					-x  :解压缩
					-C  :指定解压目录，默认为当前工作目录    

					-j  :透过 bzip2进行压缩/解压缩，压缩后的档名最好为 *.tar.bz2 
					-z  :透过 gzip进行压缩/解压缩:压缩后的档名最好为 *.tar.gz 
					-v  :显示指令执行过程
					-f filename:-f 后面跟上压缩文件
	
					--exclude=FILE:在压缩的过程中,不要将 FILE 打包!
```



- 压 缩:`tar -zcv -f filename.tar.gz file_or_folder` (后面能跟多个目录将多个目录文件打包成一个文件)
- 查 询:`tar -ztv -f filename.tar.gz`    解压前先查看，确保解压文件安全。
- 解压缩:`tar -zxv -f filename.tar.gz -C 欲解压缩到的目录`







# 提交作业



## HPC集群系统 PBS



### `qsub` 提交作业
  `qsub` 提交作业需要提供一些参数，以设定提交的节点，分配的资源，在队列中的作业名，标准输出位置，错误输出位置等设置

| 选项                                     | 描述参考                                                     |
| ---------------------------------------- | ------------------------------------------------------------ |
| `- N jobname`                            | 指定作业名，默认为脚本名                                     |
| `-l select=1:ncpus=4:host=cn1:mem=400mb` | 指定作业资源，选择cn1节点上两个块集每个块有4个cpu,分配内存400mb<br />如果不指定资源那么就没有限制。 |
| `-q queuname`                            | 绑定作业队列                                                 |
| `-l walltime=01:00:00`                   | 每个作业运行使用能够使用的最大wall-clocktime                 |
| `-o mypath/my.out`                       | 指定作业标准输出文档及路径                                   |
| `-e mypath/my.err`                       | 指定作业标准错误输文档及路径                                 |
| -j oe                                    | 标准输出与标准错误输出合流                                   |
| -W stagein=file_list                     | 在作业开始前把 file_list 复制到计算节点                      |
| -W stageout=file_list                    | 在作业完成后把 file_list 复制到计算节点                      |
| -m b                                     | 在作业开始时给用户发送邮件                                   |
| -m e                                     | 在作业结束时给用户发送邮件                                   |
| -m a                                     | 在作业中断时给用户发送邮件                                   |
| -m ba                                    | 允许用户对在同一行上带有相同标志的命令进行分组，否则只有最后一个命令被 执行 |
| -r n                                     | 指定在作业执行失败后不再重试                                 |
| -V                                       | 导入所有环境变量                                             |
| -p 300                                   | 设置优先级，数字表示优先级                                   |

* 参数可以在`qusb` 作业时候加入

  * 也可以在脚本中加入, 需要在参数前面加上PBS
    
    可以在要执行的脚本前面添加几行注释参数，标注执行设置：
    
    ```
    #!/bin/bash                 		---> bash执行该脚本
    #PBS -o filename1.out       		--->标准输出位置
    #PBS -e filename2.err       		--->错误输出位置
    #PBS -N jobname                     ---> 作业名称
    #PBS -l select=1:ncpus=10:host=cn1  --->资源分配
    mpiexec -n 1 ./run                  --->创建一个线程执行./run程序
    ```
    
    



### qstat 查看作业状态

  * `qstat` 列举出所有作业状态
  * `qstat -f job_id` 查看指定作业详细状态 

  参数：

```
-f jobid	列出指定作业的信息
-a 			列出系统所有作业
-i 			列出不在运行的作业
-n 			列出分配给此作业的结点
-s 			列出队列管理员与 scheduler 所提供的建议
-R 			列出磁盘预留信息
-Q 			操作符是 destination id，指明请求的是队列状态
-q 			列出队列状态，并以 alternative 形式显示
-au userid  列出指定用户的所有作业
-B 			列出 PBS Server 信息
-r 			列出所有正在运行的作业
-Qf queue   列出指定队列的信息
```



作业状态：

| state | 状态                                                         |
| ----- | ------------------------------------------------------------ |
| * E   | 作业在运行后退出                                             |
| * F   | 作业已完成                                                   |
| * H   | 作业被服务器或用户或者管理员阻塞                             |
| * M   | 作业已经被移动到另一个pbs server                             |
| * Q   | 作业正在排队中，等待被调度运行                               |
| * R   | 作业正在运行                                                 |
| * S   | 作业被服务器挂起，由于一个更高优先级的作业需要当前作业的资源 |
| * T   | 作业被转移到其它计算节点了                                   |
| * U   | 由于服务器繁忙，作业被挂起                                   |
| * W   | 作业在等待状态，所请求的执行时间还没到                       |
| * X   | 只用于子作业，表示子作业完成                                 |



### qdel 取消作业

指定相关作业的ID号，取消非结束态的作业。用户只能查看、删除自己提交的作业。

```
qdel <job ID>
```



###  qhold挂起作业



### qrls 取消挂起



### qorder 修改作业在队列中的顺序

`qorder <job ID1> <job ID2>` 交换治党两个作业在队列中的顺序，注意两个作业要在同PBS server中。



# 磁盘和内存
## 查看磁盘

* `ls`   只是参看inode节点记录的信息，展示文件的实际大小，以及目录的占有block大小。
  即`ls`能够显示出文件的大小，不能显示文件夹下所有文件的大小。

  ```bash
  ls -lh # l参数显示更多信息，h参数让文件大小以可读形式呈现
  ```

  例如：

  ```bash
  [xxx@cn1 codes]$ ll -lh
  drwxrwxr-x 3 xxx xxx 4.0K Mar 31 23:36 src2
  -rw-rw-r-- 1 xxx xxx 9.5M Mar 31 22:42 src2.rar
  -rw-rw-r-- 1 xxx xxx  13M Mar 31 22:48 src2.zip
  ```

  可以看到src2文件夹显示只有4.0K，但是只是该文件名占有的大小。

* `du` 该命令会递归查询目录里所有文件的大小并累加。

  `-s` 显示总计，不显示目录下文件。
  `-h` 以K,M,G为单位，提高可读性

  ```bash
  #显示当前目录下所有文件的大小（.表示当前目录，*通配所有文件名，./* 即表示当前目录下所有文件）。
  [xxx@cn1 codes]$ du -sh ./*
  173M    ./src2
  9.5M    ./src2.rar
  13M     ./src2.zip
  
  #显示src2文件夹占有大小
  [xxx@cn1 codes]$ du -sh src2
  173M    src2
  ```

  如上，通过`du`命令可以查看到当前目录下所有文件的的大小。



* `df`  显示系统磁盘分区挂载情况，以及各分区的空间大小。

  ```bash
  df - h # 加入-h参数可以将空间单位转化为人可读形式
  ```

* `lsblk`

  以树状形式列出系统的所有块设备。


## 查看内存
* `free ` 查看系统内存情况，加入`-h`参数可以将内存以方便人类看的单位显示

   ```
   [xxx@cn1 ~]$ free -h
                 total        used        free      shared  buff/cache   available
   Mem:           377G        209G        142G        144M         24G        165G
   Swap:           19G        957M         19G
   ```

  Mem 是实体内存。free是其中的空闲内存， buff/cache 是为了缩短系统I/O而设置的缓存区域，当内存不够时候系统会释放buff/cache 的空间。

  

  Swap是从磁盘划分出来的交换虚拟内存。





