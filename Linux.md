

Linux复习

Linux特点：

- 完全免费
- 完全兼容POSIX 1.0标准
- 多用户、多任务
- 良好的界面
- 丰富的网络功能
- 可靠的安全、稳定性能
- 支持多种平台

Linux组成部分:

- 内核
- Shell
- 文件系统
- 应用系统

##  1、Linux文件与目录管理

1. /etc：存放着许多系统所需的重要配置与管理文件

2. /dev：放device file（装置文件），使用者可以经由核心用来存取系统中的硬设备，当使用装置文件时内核会辨识出输入输出请求，并传递到相对应装置的驱动程序以便完成特定的动作； 

3.  /boot： 存放与系统激活的相关文件 ,不可任意删除 

4. /home : 登录用户的主目录（$HOME）放在此目录下，以用户的名称作为/home目录下各个子目录的名称。

5. /lib：存放许多系统激活时所需要的重要的共享函数库

6.  /usr/lib：存放一些应用应用程序的共享函数库，

7. /mnt：系统默认的挂载点（mount point），默认有/nnt/cdrom和/mnt/floppy

8. /proc： 虚拟文件系统，它不占用硬盘空间，目录下文件均放置于内存中；/proc记录系统进程，硬件状态、内存使用等信息。 

9. /root：系统管理用户root的主目录

10.  /bin： 存放一些系统启动时所需要的普通程序和系统程序及一些经常被其它程序调用的程序

11. /tmp：存放系统启动时产生的临时文件

12.  /var：  本目录存放被系统修改过的数据。在这个目录下的重要目录有 /var/log、/var/spool、/var/run等，它们分别用于存放记录文件、新闻邮件、运行时信息。

    

    

在Linux系统中主要根据文件头信息来判断文件类型。

### 主要文件类型

- 普通文件：文本文件内容可以直接读取，一般都是字母、数字以及一些符号等。可以使用cat、vi命令直接查看文件内容

- 纯文本文件：通常访问的文件，由ls –l命令显示出来的属性中，第一个属性为 “**-**”

- 目录文件：目录文件就是目录，相当于windows中的文件夹。由ls –l命令显示出来的属性中，第一个属性为“**d**” 

- 链接文件：符号链接相当于windows中的快捷方式。由ls –l命令显示出来的属性中，第一个属性用“**l**”表示。在Linux中有两种链接方式，符号链接和硬链接

- 设备文件：外部设备提供一种标准接口，将外部设备视为一种特殊的文件，即设备文件。在linux系统中设备文件分为**字符设备文件**和**块设备文件**   

  字符设备文件是指设备发送和接收数据以字符的形式进行  **c**开头
  块设备文件以整个数据缓冲区的形式进行。  **b**开头 
  由ls –l /dev命令显示属性 

- 套接字文件：通常用于网络数据连接。由ls –l命令显示出来的属性中，套接字文件的第一个属性用“**s**”表示 

- 管道文件：主要用来解决多个程序同时访问一个文件所造成的错误。由ls –l命令显示出来的属性中，管道文件的第一个属性用“**p**”表示 

### 文件属性

对于Linux系统的文件来说，其基本的属性有三种：读（r/4）、写（w/2）、执行（x/1） 

- 读权限：具有读取目录结构的权限，可以查看和阅读文件。
- 写权限：可以新建、删除、重命名、移动目录或文件（不过写权限受父目录权限控制）。
- 执行权限：文件拥有执行权限，才可以运行。比如二进制文件和脚本文件。有执行权限才可以进入目录文件。

### 文件操作命令:

#### 显示文件内容命令

1.  echo命令
   功能描述：输出字符串到基本输出
   语法：echo [文件名]
2. cat命令
   功能描述：用来串接文件或显示文件的内容，也可以从标准输入设备读取数据并将其结果重定向到一个新的文件中，达到建立新文件的目的。
   语法：cat [选项] [文件名]

| **选项**      |      |                      **作用**                      |
| ------------- | ---- | :------------------------------------------------: |
| -n 或 –number |      |            由1开始对所有输出的行数编号             |
| -b            |      |         和-n 相似，只不过对于空白行不编号          |
| -s            |      | 当遇到有连续两行以上的空白行，就代换为一行的空白行 |

3. more 命令
   功能描述：分页显示文件内容，在终端底部打印出“--More--”及已显示文本占全部文本的百分比。
   语法：more   [文件名]

   |  **选项**  |      | **作用**   |
   | :--------: | ---- | ---------- |
   | -f或<空格> |      | 显示下一页 |
   |   <回车>   |      | 显示下一行 |
   |   -q或-Q   |      | 退出more   |

#### 显示目录内容及更改目录命令

1. ls 命令

   功能描述：列出目录的内容 
   语法：ls [选项] [文件或目录] 

| **选项** |      | **作用**                                                     |
| -------- | ---- | ------------------------------------------------------------ |
| **-a**   |      | **显示所有文件，包括隐藏文件**                               |
| **-A**   |      | 显示所有文件，包括隐藏文件，但不列出"."和".."                |
| **-l**   |      | **使用长格式显示文件的详细信息**                             |
| **-F**   |      | **附加文件类别，符号在文件名最后**                           |
| **-d**   |      | **如果参数是目录，只显示其名称而不显示其下的各个文件**       |
| **-t**   |      | **将文件按照建立时间的先后次序列出**                         |
| **-r**   |      | **将文件以相反次序显示（默认按英文字母顺序排序）**           |
| **-R**   |      | **递归显示目录，若目录下有文件，则以下的文件也会被依序列出** |

2. pwd 命令
   功能描述：显示当前工作目录的路径 
   语法：pwd

   ![1558760763374](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760763374.png)

3. cd 命令
   功能描述：改变当前工作目录 
   语法：cd [目录] 

#### 建立、删除文件命令 

1. touch 命令
   功能描述：生成空文件和修改文件存取时间
   语法：touch  [选项] [文件名] 

| **选项** |      | **作用**                         |
| -------- | ---- | -------------------------------- |
| **-d**   |      | 以yyyymmdd的形式给出要修改的时间 |

![1558760725382](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760725382.png)

2. rm 命令
   功能描述：删除一个目录中的若干个文件或子目录语法：rm  [选项] [文件或目录] 

| **选项** |      | **作用**                           |
| -------- | ---- | ---------------------------------- |
| **-i**   |      | 互动模式，删除前再做一次确认       |
| **-r**   |      | 目录下的所有文件及子目录递归地删除 |

![1558760703697](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760703697.png)

3. mkdir 命令
   功能描述：建立目录 
   语法：mkdir  [选项] [目录名] 
   选项:  -p :依次创建目录 

![1558760664888](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760664888.png)

4. rmdir 命令
   功能描述：删除空目录 
   语法：rmdir  [选项] [目录名] 
   选项:  -p :当子目录被删除后其父目录为空目录时，也一同被删除 

   ![1558760640529](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760640529.png)

####  复制、移动命令 

1. cp 命令
   功能描述：将给出的文件或目录复制到另一文件或目录中 
   语法：cp  [选项] [源文件或目录] [目的文件或目录]

| **选项** |      | **作用**           |
| -------- | ---- | ------------------ |
| **-f**   |      | 强制复制文件       |
| **-p**   |      | 保留原文件的日期   |
| **-R**   |      | 拷贝所有文件及目录 |

![1558760610040](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760610040.png)

2. mv 命令
   功能描述：将文件或目录改名，或将文件由一个目录移入另一个目录
   语法：mv  [选项] [源文件或目录] [目的文件或目录] 

| **选项** |      | **作用**         |
| -------- | ---- | ---------------- |
| **-i**   |      | 强制复制文件     |
| **-f**   |      | 保留原文件的日期 |

![1558760559170](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760559170.png)

#### 压缩、备份命令

1.  tar 命令

   功能描述：tar是一个归档程序，可以把许多文件打包成为一个归档文件或者把它们写入备份文件 
   语法：tar  [选项] [文件或目录] 

| **选项** |      | **作用**                                   |
| -------- | ---- | ------------------------------------------ |
| **-z**   |      | 使用gzip或gunzip处理备份文件               |
| **-c**   |      | 产生一个. tar文件                          |
| **-v**   |      | 观看压缩过程                               |
| **-f**   |      | 指定压缩后的文件名                         |
| **-x**   |      | 将打包文件打开                             |
| **-t**   |      | 测试tarball压缩文件                        |
| **-z**   |      | 如果配合选项c使用是压缩，配合x使用是解压缩 |
| **-v**   |      | 将解压缩的过程显示在屏幕上                 |
| **-f**   |      | 指定解压对象为文件                         |

![1558760548932](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760548932.png)

2. gzip 命令
   功能描述：用Lempel- Ziv coding （LZ77）技术压缩文件，压缩后文件格式：. gz 
   语法：gzip  [选项] [文件] 

| **选项** |      | **作用**                              |
| -------- | ---- | ------------------------------------- |
| **-1**   |      | 是数字1，表示快速压缩                 |
| **-9**   |      | 9代表最佳状况压缩，读音nine约等于nice |
| **-r**   |      | 陆续压缩整个目录                      |

![1558760495286](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760495286.png)

![1558760514684](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760514684.png)

3. gunzip 命令

功能描述：解压缩以gzip压缩的. gz文件 
语法：gunzip  [选项] [文件或目录] 

| **选项** |      | 作用                                                         |
| -------- | ---- | ------------------------------------------------------------ |
| **-a**   |      | 使用ASCII文字模式                                            |
| **-d**   |      | 解压文件                                                     |
| **-c**   |      | 把解压后的文件输出到标准输出设备                             |
| **-f**   |      | 强行解压压缩文件，不理会文件名称或硬链接是否存在             |
| **-h**   |      | 在线帮助                                                     |
| **-l**   |      | 列出压缩文件的相关信息                                       |
| **-L**   |      | 显示版本与版权信息                                           |
| **-n**   |      | 解压文件时，若压缩文件内容含有原来的文件名称及时间戳记，则将其忽略不予处理 |

| **选项**               | **作  用**                                       |
| ---------------------- | ------------------------------------------------ |
| **-q**                 | 不显示警告信息                                   |
| **-r**                 | 递归处理，将指定目录下的所有文件及子目录一并处理 |
| **-S<压缩字尾字符串>** | 更改压缩字尾字符串                               |
| **-t**                 | 测试压缩文件是否正确无误                         |
| **-v**                 | 显示指令执行过程                                 |
| **-V**                 | 显示版本信息                                     |

![1558760381429](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760381429.png)

#### 权限管理命令

1. chgrp 命令
   功能描述：改变文件或目录的所属组 
   语法：chgrp  -R [群组] [文件或目录] 

   ![1558760365913](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760365913.png)

2. chown 命令
   功能描述：将文件或目录的所有者改变问指定用户 
   语法：chown [选项] [用户[：群组]] [文件或目录] 

   | **选项** | **作用**                                             |
   | -------- | ---------------------------------------------------- |
   | **-R**   | 递归式地改变指定目录及其下的所有子目录和文件的拥有者 |
   | **-v**   | 显示chown命令所做的工作                              |

   ![1558760315065](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760315065.png)

   ![1558760338673](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760338673.png)

3.  chmod 命令
   功能描述：改变文件或目录的访问权限 
   语法：chmod命令有两种：符号模式和绝对模式 

| **选项**                 |      | **作用**                                    |
| ------------------------ | ---- | ------------------------------------------- |
| **-c**                   |      | 只输出被改变文件的信息                      |
| **-f**                   |      | 当chmod不能改变文件模式时，不通知文件的用户 |
| **-R**                   |      | 递归地修改相应目录下所有文件和子目录        |
| **--reference=filename** |      | 参照filename的权限来设置权限                |

- 符号模式：

  命令格式：chmod [选项] [who] operator  [permission] files

  | **who**选项 |      | **含义**     |
  | ----------- | ---- | ------------ |
  | **u**       |      | 文件属主权限 |
  | **g**       |      | 属组用户权限 |
  | **o**       |      | 其他用户权限 |
  | **a**       |      | 所有用户     |

| **operator**选项 |      | **含义** |
| ---------------- | ---- | -------- |
| **+**            |      | 增加权限 |
| **-**            |      | 取消权限 |
| **=**            |      | 设定权限 |

| **permission**选项 |      | **含义** |
| ------------------ | ---- | -------- |
| **r**              |      | 读权限   |
| **w**              |      | 写权限   |
| **x**              |      | 执行权限 |

![1558760244209](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760244209.png)



- 绝对模式

  命令格式：chmod [选项] mode files

  mode是代表权限等级，由3个8进制数表示。分别代表文件属主、属组、其他用户的权限。权限数字化后，4表示读权限，2表示写权限，1表示执行权限

| 权限等级 |      | 表示权限                |
| -------- | ---- | ----------------------- |
| 7        |      | r+w+x：读、写、执行权限 |
| 6        |      | r+w：读、写权限         |
| 5        |      | r+x：读、执行权限       |
| 4        |      | r：读权限               |
| 3        |      | w+x：写、执行权限       |
| 2        |      | w：写权限               |
| 1        |      | x：执行权限             |



#### Linux文件查找命令 

1. whereis 命令
   功能描述：寻找命令的二进制文件，同时也会找到其帮助文件 
   语法：whereis [文件] 

   ```cmd
   搜索ls命令及其帮助文件的位置
   whereis ls
   ```

   

2. find 命令
   功能描述：寻找文件或目录的位置 
   语法：find [搜索路径] [搜寻关键字] [文件或目录]

| **选项**          |      | **作用**                |
| ----------------- | ---- | ----------------------- |
| **- type**        |      | 指定搜索文件的文件类型  |
| **- name**        |      | 指定搜索文件的名字      |
| **- group gname** |      | 搜索组名称为gname的文件 |
| **- iname**       |      | 与-name类似             |

```cmd
例：从根目录寻找file的位置并把输出显示到屏幕上 
sudo find / -name file
例：在/etc目录下，搜寻所有以fir开头的文件
sudo find /etc -iname 'fir*'
例：在/etc目录下，搜索所有以f开头后面有四个字符的文件 
sudo find /etc -iname 'f????'
```

![1558760788877](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760788877.png)

3.  locate 命令
   功能描述：寻找文件或目录
   语法：locate [搜索关键字]

列出所有和abc相关的文件，并用more程序显示

![1558760828113](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558760828113.png)



## 2、Linux系统用户管理

系统有一个数据库，存放着用户名与uid的对应关系，这个数据库存在配置文件/etc/passwd中

#### 用户分类：

1. 普通用户：通常把/bin/bash作为登录shell，把/home作为用户主目录。一般情况下，普通用户只在自己的主目录和系统范围内的临时目录里创建文件。
2. 超级用户：超级用户uid为0，使用/root作为主目录，在系统上有完全权限：
   -  可以修改和删除任何文件
   - 可以运行任何命令
   - 可以取消任何进程
   - 超级用户负责增加和保留其他系统用户

3. 系统用户：大多数Linux系统会将一些低uid保留给系统用户 
   -  系统用户代表系统的组成部分
   - 系统用户通常没有登录shell
   - 系统用户的主目录很少在/home中，而通常在属于相关应用的系统目录中。例如，用户apache的目录/var/www

| 用户id范围 | **用户类型** |
| ---------- | ------------ |
| 0          | 根用户       |
| 1~499      | 系统用户     |
| 500+       | 普通用户     |

Linux操作系统把全部用户信息保存为普通的文本文件：**passwd**文件、**shadow**文件、**group**文件、**gshadow**文件。
       这些文件可以通过文本编辑器查看 。 

### 用户和用户组

#### password文件

用户的关键信息被存放在系统的/etc/passwd文件中，系统的每一个合法用户账号对应于该文件中的一行记录，记录定义了每个用户账号的属性。用户数据按字段以冒号分隔。

格式：username：password：uid：gid：userinfo：home：shell

| **字段名**   | **编号** | **说明**                                |
| ------------ | -------- | --------------------------------------- |
| **username** | 1        | 给一个用户可读的用户名称                |
| **password** | 2        | 加密的用户密码                          |
| **uid**      | 3        | 用户ID，Linux内核用这个整数来识别用户   |
| **gid**      | 4        | 用户组ID，Linux内核用这个整数识别用户组 |
| **userinfo** | 5        | 用来保存帮助识别用户的简单文本          |
| **home**     | 6        | 当用户登录时，分配给用户的主目录        |

![1558778003025](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558778003025.png)

在Linux和Unix系统中，采用“影子密码”技术来保存密码，用户的密码被保存在专门的/etc/shadow文件中。查看该文件需要超级管理员root的权限。 

#### shadow文件

/etc/shadow文件中的每行记录一个合法用户账号的数据，每一行的数据用冒号分隔 

   格式：username：password：lastchg：min：max：warn：inactive：expire：flag 

| **字段名**   | **编号** | **说  明**                             |
| ------------ | -------- | -------------------------------------- |
| **username** | 1        | 用户的登录名                           |
| **password** | 2        | 加密的用户密码                         |
| **lastchg**  | 3        | 自1970.1.1起到上次修改口令所经过的天数 |
| **min**      | 4        | 两次修改口令之间至少经过的天数         |
| **max**      | 5        | 口令还会有效的最大天数                 |
| **warn**     | 6        | 口令失效前多少天内向用户发出警告       |
| **inactive** | 7        | 禁止登录前用户还有效的天数             |
| **expire**   | 8        | 用户被禁止登录的时间                   |
| **flag**     | 9        | 保留                                   |

#### group文件

/etc/group文件对组的作用相当于/etc/passwd文件对用户的作用

 格式：group_name：group_password：group_id：group_members

| **字段名**         | **编号** | **说明**           |
| ------------------ | -------- | ------------------ |
| **group_name**     | 1        | 用户组名           |
| **group_password** | 2        | 加密后的用户组密码 |
| **group_id**       | 3        | 用户组ID           |
| **group_members**  | 4        | 逗号分隔开的组成员 |

![1558777980816](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558777980816.png)

#### gshadow文件

用户组文件也采用将组口令与组的其它信息分离的安全机制，即使用/etc/gshadow文件存储加密的组口令。
查看这个文件需要**root**的权限 

格式：group_name：group_password：group_id：group_members 

| **字段名**         | **编号** | **说明**                       |
| ------------------ | -------- | ------------------------------ |
| **group_name**     | 1        | 用户组名                       |
| **group_password** | 2        | 加密后的用户组密码             |
| **group_id**       | 3        | 用户组ID（可以为空）           |
| **group_members**  | 4        | 逗号分隔开的组成员（可以为空） |



![1558778073197](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558778073197.png)



### 用户管理命令

#### useradd命令

- 功能描述：在Linux系统中创建新用户
-  语法：useradd [选项] 用户名 

| **选项** | **作用**                                                     |
| -------- | ------------------------------------------------------------ |
| **-d**   | 指定用户主目录                                               |
| **-g**   | 指定gid                                                      |
| **-u**   | 指定uid                                                      |
| **-l**   | 不要把用户添加到lastlog和failog中，这个用户的登录记录不需要记载 |
| **-M**   | 不要建立用户主目录                                           |
| **-m**   | 自动创建用户主目录                                           |
| **-p**   | 指定新用户的密码                                             |
| **-r**   | 建立一个系统帐号                                             |
| **-s**   | 指定shell                                                    |

例子：使用useradd创建一个test用户。用户组为ycs，登录shell为/bin/bash，用户主目录为/home/Test 

![1558778311190](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558778311190.png)



使用useradd时，后面不添加任何参数选项，创建 “三无”用户：一无主目录，二无密码，三无系统Shell。



#### password命令

- 功能描述：为新增加的用户设置口令，也可以更改原有用户的口令，管理员还可以使用passwd命令锁定某个用户账户 
- 语法：passwd [选项] 用户名 

| **选项** | **作用**                         |
| -------- | -------------------------------- |
| **-l**   | 管理员锁定已经命名的账户名称     |
| **-u**   | 管理员解开账户锁定状态           |
| **-x**   | 管理员设置最大密码使用时间（天） |
| **-n**   | 管理员设置最小密码使用时间（天） |



例：为新建用户test设定密码 ![1558778534408](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558778534408.png)



#### usermod命令

- 功能描述：修改用户账户的信息 
- 语法：usermod [选项] 用户名

| **选项** | **作用**                           |
| -------- | ---------------------------------- |
| **-d**   | 修改用户主目录                     |
| **-e**   | 修改帐号的有效期限                 |
| **-f**   | 修改在密码过期后多少天即关闭该帐号 |
| **-g**   | 修改用户所属的组                   |
| **-G**   | 修改用户所属的附加组               |
| **-l**   | 修改用户帐号名称                   |
| **-L**   | 锁定用户密码，使密码无效           |
| **-s**   | 修改用户登入后所使用的shell        |
| **-u**   | 修改用户ID                         |
| **-U**   | 解除密码锁定                       |

例：将test用户添加到组users中

![1558778707529](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558778707529.png)

修改 test的用户名为test2 

![1558778718143](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558778718143.png)



#### userdel 命令 

- 功能描述：删除系统中的用户 
- 语法：userdel [选项] 用户名 
- 选项:   -r  删除账户时，连同用户主目录一起删除 



例：删除test1账户，并将用户主目录一同删除

![1558778762636](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558778762636.png)



### 用户组管理命令

#### groupadd 命令 

- 功能描述：指定组名称来建立新的组账号 
- 语法：groupadd [选项] 组名 

| **选项** | **作用**                               |
| -------- | -------------------------------------- |
| **-g**   | 组id，除非使用-o选项，否则该值必须唯一 |
| **-o**   | 允许设置相同组id的群组                 |
| **-r**   | 建立系统组                             |
| **-f**   | 强制执行，创建相同id的组               |

例：新建组helo，指定gid为5000 

![1558778896695](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558778896695.png)



#### groupmod 命令

- 功能描述：修改用户组属性
- 语法：groupmod [选项] 组名 

| **选项** | **作用**       |
| -------- | -------------- |
| **-g**   | 指定组id       |
| **-o**   | 与groupadd相同 |
| **-n**   | 修改用户组名   |

例：修改组helo的组名为ehlo，gid为6000

![1558778979913](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558778979913.png)



#### groupdel 命令 

- 功能描述：从系统上删除组。如果该组中仍包含某些用户，则必须先删除这些用户后，方能删除组。 
- 语法：groupdel 组名 

例：为组ehlo添加新用户wangli，然后删除组ehlo

![1558779049954](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558779049954.png)



### su和sudo命令

#### su命令

- 功能描述：切换用户。超级权限用户root向普通或虚拟用户切换不需要密码，而普通用户切换到其它任何用户都需要密码验证
- 语法：su  [选项] 用户名

| **选项** | **作用**                                                 |
| -------- | -------------------------------------------------------- |
| **-l**   | 切换用户时，如同重新登陆，如果没有指定用户名，默认为root |
| **-p**   | 切换当前用户时，不切换用户工作环境，此为缺省值           |
| **-c**   | 以指定用户身份执行命令                                   |
| **-**    | 切换当前用户时，切换用户工作环境                         |

例：切换用户，并切换用户工作环境

![1558779151901](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1558779151901.png)





#### sudo 命令 

- 功能描述：允许超级权限用户root为其他用户委派权利，使之能运行部分或全部由root用户执行的命令 
- 语法：sudo  [选项] 命令

| **选项** | **作用**                                        |
| -------- | ----------------------------------------------- |
| **-h**   | 列出帮助信息                                    |
| **-V**   | 列出版本信息                                    |
| **-l**   | 列出当前用户可以执行的命令                      |
| **-u**   | 以指定用户的身份执行命令                        |
| **-k**   | 清除timestamp文件，下次使用sudo时需要再输入密码 |
| **-b**   | 在后台执行指定的命令                            |
| **-p**   | 更改询问密码的提示语                            |
| **-e**   | 不是执行命令，而是修改文件，相当于命令Sudoedit  |



## 3、磁盘管理

磁盘的物理结构：

1.  磁道
2. 扇区
3. 柱面
4. 簇

扇区是硬盘数据存储的最小单位。

操作系统将相邻的扇区组合在一起，形成一个簇，再对簇进行管理。

每个簇可以包括2、4、8、16、32、64个扇区。



Linux系统中，每一个设备都映射到一个系统文件：

- IDE设备  分配了一个有hd前缀组成的文件
-   SCSI设备分配了一个有sd前缀组成的文件 
    编号方法按照英文字母表顺序，如hda、hdb; sda、sdb、sdc等 



#### 查看硬盘信息

sudo fdisk –l查看分区表信息

![1559118255744](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1559118255744.png)





#### 创建磁盘分区

fdisk命令参数：

| **参数** | **说明**               |
| -------- | ---------------------- |
| **a**    | 设置分区为启动分区     |
| **d**    | 删除分区               |
| **l**    | 显示支持的分区类型     |
| **m**    | 显示帮助信息           |
| **n**    | 新建分区               |
| **p**    | 显示磁盘的分区表       |
| **q**    | 不保存退出             |
| **t**    | 改变分区的类型号码     |
| **u**    | 改变分区大小的显示方式 |
| **v**    | 检验磁盘的分区列表     |
| **w**    | 保存退出               |
| **x**    | 进入专家模式           |



执行sudo fdisk /dev/sdb命令对sdb分区，

在分区的过程中，一般先键入“m”，查看参数说明

通过“p”参数，查看硬盘的分区表信息，根据分区表信息确定接下来的分区 

通过“n”来新建分区，分区类型为主分区，分区编号为1，起始扇区默认2048，最后扇区8388608，分区大小为4G 

看到sdb这块硬盘已经分成两个分区sdb1和sdb2，分区完成后，使用“w”保存退出 



分区完成后，需要对分区格式化、创建文件系统才能正常使用。格式化分区的主要命令是mkfs，格式为：

mkfs –t [文件系统格式] 设备名

选项-t的参数用来指定文件系统格式，如ext3，nfs等
       设备名称如/dev/sdb1，/dev/sdb2等 



![1559118486474](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1559118486474.png)

在使用磁盘分区前，需要挂载该分区。挂载时，需要指定挂载的设备和挂载点

挂载点就是目录文件，一般放在/mnt或者/media目录下。挂载磁盘分区的命令mount格式为：

mount [选项] 设备名 挂载点

- mount命令常用的选项有：
  -a	加载文件/etc/fstab中设置的所有设备
  -f	不实际加载设备
  -F	需与-a参数同时使用
  -h	显示在线帮助信息
  -n	不将加载信息记录在/etc/mtab文件中
  -o	指定加载文件系统时的选项
  -t     指定设备的文件系统类型。
- 

![1559118567011](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1559118567011.png)



挂载 usb

在/mnt目录下新建/mnt/usb目录，作为usb移动设备的挂载点，插入usb设备后，linux系统将其识别为SCSI设备，分区自动命名为/dev/sdc1，使用mount命令挂载 

![1559118607811](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1559118607811.png)



​    卸载磁盘分区

卸载磁盘的命令为umount ，格式为：

umount  设备名或挂载点



# 3、进程管理

Ubuntu系统的运行级别与其他Linux系统的运行级别有些区别：

| **运行级别** | **含义**                 |
| ------------ | ------------------------ |
| **0**        | **关机**                 |
| **1**        | **单用户模式**           |
| **2-5**      | **图形界面的多用户模式** |
| **6**        | **重新启动**             |

Ubuntu系统的运行级别2～5级是一样的，默认运行级别是2，这与其他Linux系统是不同的。比如Redhat Linux的运行级别中2、3是字符界面，默认运行级别是3 



### 关闭系统

使用shutdown命令关闭系统，格式为：
          shutdown [选项]   

| **参数** | **作用**                                                     |
| -------- | ------------------------------------------------------------ |
| **-t**   | 关机倒计时（秒）                                             |
| **-**r   | 系统关闭后重启                                               |
| **time** | 设置多久时间后执行shutdown命令。可以用绝对时间，如hh：mm，或用相对时间，如+mm，如果要立即执行则用now表示。 |
| **-c**   | 将前一个shutdown命令取消                                     |



### 物理内存和虚拟内存 

- 物理内存：系统硬件提供的内存大小
- 虚拟内存：使用硬盘作为物理内存RAM的扩展，在硬盘空间中虚拟出的一块逻辑内存，使可用内存相应地有效扩大。 
- 交换分区（Swap Space）：用作虚拟内存的磁盘空间



首先，Linux系统会不时的进行页面交换操作，以保持尽可能多的空闲物理内存 

其次，linux内核根据“最近最经常使用”算法，将一些不经常使用的页面文件交换到虚拟内存 

最后，交换分区的页面在使用时会首先被交换到物理内存



### 内存的监视

监视内存最常使用的命令有free、top等

使用free查看内存的使用状态 

![1559119030103](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\1559119030103.png)

- Mem：代表物理内存使用情况。
  -/+ buffers/cached：代表磁盘缓存使用状态。
  Swap：交换分区内存使用状态。
-   total：物理内存的总大小。 
    used：已经使用的物理内存为。 
    free：空闲的物理内存。 
    shared：多个进程共享的内存。
    buffers/cached：磁盘缓存的大小 



### 常用进程管理命令

用ps命令查看进程 

| **选项**                    | **列出的进程**           |
| --------------------------- | ------------------------ |
| **-A**，-e，-ax             | 所有进程                 |
| **-C command**              | 所有command的实例        |
| **-U**，--user，--User user | 属于user的所有进程       |
| **-t**，--tty terminal      | 从terminal启动的所有进程 |

- 输出选择

| **选项**                        | **输出格式**                                |
| ------------------------------- | ------------------------------------------- |
| **-f**                          | **详尽列表**                                |
| **-l**，**1**                   | **长格式**                                  |
| **-j**，**j**                   | **作业格式**                                |
| **-o**，**o**，**--format str** | **使用由**str**指定的字段，由用户定义格式** |

- 修改所选信息的显示方式

| **选项**        | **输出格式**                        |
| --------------- | ----------------------------------- |
| **-H**          | **显示进程层数**                    |
| **f, --forest** | **显示包括**ASCII**修饰的进程层次** |
| **h**           | **不打印标题行**                    |
| **-w**          | “宽”输出（包含较长命令名）          |



  用top命令监控进程 

top命令用来监控Linux进程的整体状态，从终端中运行，用当前运行进程一览表取代命令行，每隔几秒更新一次，对任何按下的单键做出反应 

| **q**     | 退出                                 |
| --------- | ------------------------------------ |
| **h or?** | 帮助                                 |
| **s**     | 设定两次更新之间的时间（以秒为单位） |
| **space** | 更新显示                             |
| **M**     | 根据内存大小对进程排序               |
| **P**     | 根据CPU（处理器）占用对进程排序      |
| **u**     | 显示特定用户的进程                   |
| **k**     | 杀死进程（给进程发送信号）           |

| **选项**      | **作用**                                         |
| ------------- | ------------------------------------------------ |
| **-d secs**   | **在两次刷新之间延迟**secs秒（默认为5秒）        |
| **-q**        | **尽量经常刷新**                                 |
| **-n**，**N** | **刷新**N**次后退出**                            |
| **-b**        | **以“批处理方式”运行，好像是在哑终端上写入一样** |

 使用kill命令结束进程

kill命令用来向其他进程发送自定义信号，使用数字或符号命令行选项（指定要发送的信号）和进程id（指定接收信号的进程)来调用

| **选项** | **作用**       |
| -------- | -------------- |
| **-s**   | 指定发送的信号 |
| **-p**   | 模拟发送信号   |
| **-l**   | 信号的名称列表 |

 用nice启动低优先级命令 

用renice改变正在运行的进程 

| **选项** | **作用**                            |
| -------- | ----------------------------------- |
| **-p**   | **将剩余参数解释为**pid**（默认）** |
| **-u**   | **将剩余参数解释为用户名**          |
| **-g**   | **将剩余参数解释为**gid             |

 jobs命令显示后台执行的任务 

| **选项** | **作用**               |
| -------- | ---------------------- |
| **-p**   | 列出进程ID             |
| **-n**   | 列出发生变化的进程ID   |
| **-l**   | 列出后台进程的所有信息 |



# 4.Linux编辑器的使用

- 启动vi编辑器：在命令提示符状态下，输入
  vi [文件名]
  如果不指定文件名，则新建一个未命名的文本文件

| **命令**                       | **功能**                                            |
| ------------------------------ | --------------------------------------------------- |
| **vi filename**                | **打开或新建文件，并将光标置于第一行首**            |
| **vi +n filename**             | **打开文件，并将光标置于第**n**行首**               |
| **vi + filename**              | **打开文件，并将光标置于最后一行首**                |
| **vi + /str filename**         | **打开文件，并将光标置于第一个与**str**匹配的串处** |
| **vi** **–**r filename         | **在上次使用**vi**编辑时系统崩溃，恢复**filename    |
| **vi filename1**…**filenamen** | **打开多个文件，依次编辑**                          |

​	

vi有3种基本工作模式：

1. 命令行模式
2. 输入模式 

3. 末行模式 





输入模式：编辑文件内容

命令行进入输入模式的按键：

| **命令** | **功能**                                        |
| -------- | ----------------------------------------------- |
| **i**    | **从目前光标所在处插入**                        |
| **I**    | **从目前所在行的第一个非空格符处开始插入**      |
| **a**    | **从目前光标所在的下一个字符处开始插入**        |
| **A**    | **从光标所在行的最后一个字符处开始插入**        |
| **o**    | **从目前光标所在行的下一行处插入新的一行**      |
| **O**    | **从目前光标所在处的上一行插入新的一行**        |
| **r**    | **替换光标所在的那一个字符一次**                |
| **R**    | **替换光标所在处的文字，直到按下**Esc**键为止** |

末行模式

- 命令行模式下按“：”键进入末行模式，提示符为 “：” 
  末行命令执行后，vi自动回到命令模式。若在末行模式的输入过程中，可按退格键将输入的命令全部删除，再按一下退格键，即可回到命令模式。 

| **:w**                         | **将编辑的数据保存到文件中**                           |
| ------------------------------ | ------------------------------------------------------ |
| **:w!**                        | **若文件属性为“只读”时，强制写入该文件**               |
| **:q**                         | **退出**vi                                             |
| **:q!**                        | **强制退出不保存文件**                                 |
| **:wq**                        | **保存后退出**vi                                       |
| **:w filename**                | **将编辑的数据保存成另一个文件**                       |
| **/word**                      | **向下寻找一个名称为**word**的字符串**                 |
| **?word**                      | **向上寻找一个名称为**word**的字符串**                 |
| **n**                          | **n**为按键，代表重复前一个查找的操作**                |
| **N**                          | **N**为按键，与**n**相反，为“反向”进行前一个查找操作** |
| **:n1**，**n2s/word1/word2/g** | **在第**n1与n2行之间寻找word1字符串，并替换为word2     |
| **:1  ，$s/word1/word2/g**     | **全文查找**word1字符串，并将该它替换为word2           |

- vi编辑器的三种工作模式之间的转换：
  （1）命令行模式→输入模式：i，I，a，A
  （2）输入模式→命令行模式：Esc
  （3）命令行模式→末行模式：：

| **h**或向左箭头键       | **光标向左移动一个字符**                             |
| ----------------------- | ---------------------------------------------------- |
| **j**或向下箭头键       | **光标向下移动一个字符**                             |
| **k**或向上箭头键       | **光标向上移动一个字符**                             |
| **l**或向右箭头键       | **光标向右移动一个字符**                             |
| **+**                   | **光标移动到非空格符的下一行**                       |
| **-**                   | **光标移动到非空格符的上一行**                       |
| **n<space>**            | **按下数字**n**后再按空格键，光标会向右移**n**个字符 |
| **0****或功能键**Home** | **移动到这一行的行首**                               |
| **$****或功能键**End**  | **移动到这一行的行尾**                               |
| **H**                   | **光标移动到屏幕的第一行的第一个字符**               |
| **M**                   | **光标移动到屏幕的中央的那一行的第一个字符**         |
| **L**                   | **光标移动到屏幕的最后一行的第一个字符**             |
| **G**                   | **光标移动到这个文件的最后一行**                     |
| **nG**                  | **n**为数字。移动到这个文件的第**n**行               |
| **gg**                  | **移动到这个文件的第一行。相当于**1G                 |
| **n[Enter]**            | **n**为数字。光标向下移动**n**行                     |



### 屏幕操作命令

以屏幕为单位的光标操作，常用于滚屏和分页

| **按键**     | **功能**                                    |
| ------------ | ------------------------------------------- |
| **[Ctrl]+f** | **屏幕向下移动一页，相当于[Page Down]**按键 |
| **[Ctrl]+b** | **屏幕向上移动一页，相当于[Page Up]**按键   |
| **[Ctrl]+d** | **屏幕向下移动半页**                        |
| **[Ctrl]+u** | **屏幕向上移动半页**                        |

### 文本修改命令

| **按键** | **功能**                                                     |
| -------- | ------------------------------------------------------------ |
| **x**    | **删除光标所在位置上的字符**                                 |
| **dd**   | **删除光标所在行**                                           |
| **n+x**  | **向后删除**n个字符，包含光标所在位置                        |
| **n+dd** | **向下删除**n行内容，包含光标所在行                          |
| **yy**   | **将光标所在行复制**                                         |
| **n+yy** | **将从光标所在行起向下的n行复制**                            |
| **n+yw** | **将从光标所在位置起向后的**n个字符串(单词)复制              |
| **p**    | **将复制**(或最近一次删除)的字符串(或行粘贴在当前光标所在位置** |
| **u**    | **撤销上一步操作**                                           |
| **.**    | **重复上一步操作**                                           |



在vi中设置一下行号。在末行模式输入：set nu 