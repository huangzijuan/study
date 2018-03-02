1.定时执行任务
1)创建用户ttt useradd ttt
2)给ttt设置密码 passwd ttt
3)用户ttt创建定时任务，在/tmp下创建一个新文件 crontab -u ttt -e
进入界面后按照 分 时 日期 月份 星期 touch /tmp/新文件
4)等待事件发生后到相应目录下查看新文件创建时间等是否正确等到时间后查看文件是否创建成功

2.用户权限设置
1)创建3个用户：nihao、tahao、wohao useradd nihao passwd nihao useradd tahao passwd tahao useradd wohao passwd wohao
2)用nihao、tahao用户分别创建目录/tmp/nihao、/tmp/tahao su nihao mkdir /tmp/nihao su tahao mkdir /tmp/tahao
3)用nihao在/tmp/nihao下创建文件nihao_tmp su nihao touch /tmp/nihao/nihao_tmp
4)用tahao在/tmp/nihao下创建文件tahao_tmp可以吗？ su tahao touch /tmp/nihao/tahao_tmp 这样会出现权限不够的提示，正常，否则就是出错了
5)用root用户修改目录nihao的属性为g+s su root chmod g+s /tmp/nihao
6)创建用户other，并把他加入到组nihao里 useradd other usermod -G nihao other
7)用other在/tmp/nihao下创建文件other_tmp su other touch /tmp/nihao/other_tmp
8)查看文件other_tmp的文件主和文件属主，和文件nihao_tmp一样吗？这就是属性g+s的作用 ls -l /tmp/nihao/other_tmp ls -l /tmp/nihao/nihao_tmp
9)将tahao设为公共目录，用nihao创建文件nihao_tmp到这个公共目录下、用wohao创建文件wohao_tmp chmod 777 /tmp/tahao su nihao touch /tmp/tahao/nihao_tmp su wohao touch /tmp/tahao/wohao_tmp
10)尝试用nihao去删除wohao_tmp,可以吗？ su nihao rm /tmp/tahao/wohao_tmp 可以删除
11)如果wohao_tmp删掉，重新创建它 touch /tmp/tahao/wohao_tmp
12)把tahao属性进一步设为o+t chmod o+t /tmp/tahao 给予其他用户组保存程序的文本到交换设备上的权限
13)尝试用nihao去删除wohao_tmp,可以吗？ su nihao rm /tmp/tahao/wohao_tmp 应该不可以删除

3.创建分区，建立文件系统并挂载
1)查看当前分区 fdisk -l
2)编辑分区表，新建分区 fdisk /dev/sda 输入 n 输入分区大小输入 w保存退出 fdisk -l 查看/前提是在root权限下
3)分区表写回内存 partprobe /dev/sda
4)对新建的分区创建新的文件系统ext3 mkfs -t ext3 -L 文件系统名称 /dev/sda4(以自己的分区为主)
5)建立挂载点/mnt/data mkdir /mnt/data
6)将新的文件系统挂到挂载点上 mount -o rw LABEL=文件系统名称 /mnt/data
7)编辑文件/etc/fstab，使得系统启动时新的分区自动挂载这个不会
8)查看挂载信息 df -h

4.脚本编写，实现与用户交互
1)创建目录/tmp/scripts mkdir /tmp/scripts
2)在目录下创建脚本文件，自行命名，脚本文件实现与用户交互
3)调用脚本，验证编写脚本是否正确

5.脚本编写，实现两数相乘，并调用执行
1)创建目录/tmp/scripts
2)在目录下创建脚本文件，自行命名，脚本文件实现两数相乘 vi ex1 echo "enter your first number" read x echo "enter your second number" read y ((z=x*y)) echo "the answer is $z" :wq
3)调用脚本，验证编写脚本是否正确 bash ex1

6.脚本编写，
功能为：查找某文件是否存在（以参数形式），若存在，则将其权限设置为用户主可读可改，其他人无任何权限。否则则返回无此文件的信息。
1)创建目录/tmp/scripts
2)在目录下创建脚本文件，自行命名，脚本文件实现题干功能 vi ex2 echo "please enter your file name" read x if test -f "$x" then chmod 600 $x else echo "can not found the file" fi
3)调用脚本，验证编写脚本是否正确 bash ex2

7.脚本编写，
功能为：计算从1加到100的和并返回结果。
1)创建目录/tmp/scripts
2)在目录下创建脚本文件，自行命名，脚本文件实现题干功能 vi ex3 ((x=0)) echo "计算1---100的和" for((i=1;i<=100;i++)) do ((x+=i)) done echo "the answer is $x"
3)调用脚本，验证编写脚本是否正确 bash ex3

8.Vi的使用
1)在/tmp目录下建立一个名为vitest的目录 mkdir /tmp/vitest
2)进入vitest目录中 cd /tmp/vitest
3)将/etc/man.comfig复制到本目录中 cp /etc/man.config .
4)使用vi打开本目录下的man.config文件 vi man.config
5)在vi中设置行号 set nu
6)移动到第58行，向右移动40个字符，请问双引号内是什么目录？ 58G 40l
7)移动到第一行，并且向下搜索“bzip2”字符串，请问它在第几行？ 1G :/bzip2
8)接下来要将50～100行的man改为MAN，并且一个一个挑选是否需要修改，如何执行命令？ :50,100 s /man/MAN/gc
9)修改完之后 ，突然反悔了，要全部复原 ，有哪些办法？ :U
10)要复制 51～60的内容，并且贴到最后一行之后 51G 10yy G p
11)删除11～30行之间的20行 11G 20dd
12)将这个文件另存为man.test.config文件 :w man.test.config
13)到第29行，并且删除15个字符 29G 15x
14)储存后离开 :wq
