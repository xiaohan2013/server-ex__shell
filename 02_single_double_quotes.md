## 单引号和双引号

单引号和双引号其实差不多，主要泣别如下：
‘’单引号：凡是单引号内的所有特殊字符都无效
”“双引号：在双引号内的特殊字符大部分无效，有些则会保留，比如$ \等
例如：
[wang@localhost ~]$ A=B C
bash: C: command not found
[wang@localhost ~]$ A="B C"
[wang@localhost ~]$ echo $A
B C
[wang@localhost ~]$ echo "$A"
B C
[wang@localhost ~]$ echo '$A'
$A

例如：
[wang@localhost ~]$ A=B\ C
[wang@localhost ~]$ echo '"$A"'
"$A"
[wang@localhost ~]$ echo "'$A'"
'B C'


## 反斜杠

反斜杠，只有紧接着的特殊字符才无效
例如：
[wang@localhost ~]$ A=B\
> C\
> 
[wang@localhost ~]$ echo $A
BC

如果要让转义字符起作用，就要使用-e，且转义字符要使用双引号。
例如：
[wang@localhost ~]$ echo -e "\n"


[wang@localhost ~]$ 

## 反引号

在反引号中的命令代表了命令执行后的标准输出。
例如：
[wang@localhost ~]$ echo the pwd is `pwd`
the pwd is /home/wang