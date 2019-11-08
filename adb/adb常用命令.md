## 参数含义
一般来说内存占用大小有如下规律：VSS >= RSS >= PSS >= USS

VSS - Virtual Set Size 虚拟耗用内存（包含共享库占用的内存）
RSS - Resident Set Size 实际使用物理内存（包含共享库占用的内存）
PSS - Proportional Set Size 实际使用的物理内存（比例分配共享库占用的内存）
USS - Unique Set Size 进程独自占用的物理内存（不包含共享库占用的内存

## 常用命令
1. top  | grep app名称  （-t 显示进程名称，-s 按指定行排序，-n 在退出前刷新几次，-d 刷新间隔，-m 显示最大数量）
2. ps  |  grep app名称
3. procrank | grep app名称  （eg：adb shell procrank | grep com.package > appmem）
4. dumpsys meminfo app名称
前两个命令只能查到VSS RSS内存占用信息，而后面两个命令可以查出  PSS USS内存占用.
dumpsys meminfo 可以查出native和dalvik分别占用多少内存

## dumpsys （用来给出手机中所有应用程序的信息，并且也会给出现在手机的状态。）
dumpsys [Option]
        meminfo 显示内存信息
        cpuinfo 显示CPU信息
        account 显示accounts信息
        activity 显示所有的activities的信息
        window 显示键盘，窗口和它们的关系
        wifi 显示wifi信息

## 其它参考
http://gityuan.com/2016/02/27/am-command/
