## 重定向

FD(file Descriptor)
0: starndard Input(STDIN)
1: starndard Onput(STDOUT)
2: starndard Error Onput(STDERR)


stdin(0): keyboard  键盘输入,并返回在前端 
stdout(1): monitor  正确返回值 输出到前端 
stderr(2): monitor 错误返回值 输出到前端 

一般来说, "1>" 通常可以省略成 ">". 
有了这些认识才能理解 "1>&2" 和 "2>&1". 

1>&2  正确返回值传递给2输出通道 &2表示2输出通道 
如果此处错写成 1>2, 就表示把1输出重定向到文件2中.
2>&1 错误返回值传递给1输出通道, 同样&1表示1输出通道.

举个例子. 
[root@redhat box]# ls a.txt b.txt 1>file.out 2>&1 
[root@redhat box]# cat file.out 
ls: b.txt: No such file or directory 
a.txt 
现在, 正确的输出和错误的输出都定向到了file.out这个文件中, 而不显示在前端. 
补充下, 输出不只1和2, 还有其他的类型, 这两种只是最常用和最基本的.

问：Linux重定向中 >&2 怎么理解？
问题补充：echo "aaaaaaaaaaaaaaaa" >&2 怎么理解？
答：
>&2  即 1>&2 也就是把结果输出到和标准错误一样；之前如果有定义标准错误重定向到某log文件，那么标准输出也重定向到这个log文件
如：ls 2>a1 >&2  （等同 ls >a1 2>&1）
把标准输出和标准错误都重定向到a1，终端上看不到任何信息。

0:表示键盘输入(stdin)
1:表示标准输出(stdout),系统默认是1 
2:表示错误输出(stderr)

command >/dev/null 2>&1 &  == command 1>/dev/null 2>&1 &

1)command:表示shell命令或者为一个可执行程序
2)>:表示重定向到哪里 
3)/dev/null:表示Linux的空设备文件 
4)2:表示标准错误输出
5)&1:&表示等同于的意思,2>&1,表示2的输出重定向等于于1
6)&:表示后台执行,即这条指令执行在后台运行
 
1>/dev/null:表示标准输出重定向到空设备文件,也就是不输出任何信息到终端,不显示任何信息。
2>&1:表示标准错误输出重定向等同于标准输出,因为之前标准输出已经重定向到了空设备文件,所以标准错误输出也重定向到空设备文件。

这条命令的意思就是在后台执行这个程序,并将错误输出2重定向到标准输出1,然后将标准输出1全部放到/dev/null文件,也就是清空.
所以可以看出" >/dev/null 2>&1 "常用来避免shell命令或者程序等运行中有内容输出。