# Linux基础第三弹

## 扩展正则表达式：

扩展正则表达式：egrep=grep -E

## vim使用：
vim：命令模式，插入模式，扩展模式

扩展模式：r file：将某文件读入当前文件光标后

脚本中默认不支持别名

unset “num1”：删除num1这个变量

echo $$ :查看当前在哪个进程

echo $BASHPID 同上（更精准，例如在子shell中）

## 变量形式：

普通变量：无法在子进程下使用只对当前生效

环境变量：对子进程生效

export name=VALUE ：定义环境变量

export：查看系统中所有环境变量

dirname /etc/rc.d/init.d/functions：取出此文件的目录并显示

basename /etc/rc.d/init.d/functions：取出此文件的文件名并显示

## 基础脚本

 #！/bin/bash：脚本中的shebang机制，加入此机制可以明确脚本所使用bash，调用变量是如果不是环境变量不加shebang机制将无法显示（建议追加）

$SHLVL:可查看bash的嵌套层数

$_:前一个命令的最后一个字符串将进行赋值

$PPID：父进程进程号

readonly 常量名=赋值：设置为只读变量，不可修改不可删除（logout即失效）可以先赋值在声明

readonly -p：显示常量

位置变量：

$*:显示所有参数

$@：同上

$#:参数个数

$0：显示脚本目录

set --：清除所有参数

$?:查看前一条命令是否成功，结果为0即为成功，非0即为失败

.或source：执行脚本，会在当前shell中执行

bash或脚本名称：在子shell中执行

expr 4 + 3：算数表达式，参数之间必须加空格，称号要转义

在/etc/建立nologin文件，普通用户将不能登陆系统

命令：
locate 文件名：搜索文件，搜索locate数据库而不是搜索文件，新生文件将无法搜索没有即时性
updatedb：更新locate数据库（数据库文件位置/var/lib/mlocate/mlocate.db）
-r ：支持正则表达式（基本正则表达式）

## 搜索：

find / -size 10M :搜索/下10m的文件（不是具体的10M而是10M-1到10M）

find -perm /644 ：或的关系，满足三项其一即可也可高于

find -perm -644 ：与的关系，需三项权限高于或等于此权限

find -prem 644 ：准确搜索此权限的文件

xargs：在命令不支持管道传递参数的时候可以使用，或者有些命令不支持过多参数的时候，xargs会将某个命令产生的参数逐个进行处理

## 压缩：

gzip [option] file :压缩文件，压缩完成后原文件删除（压缩与解压缩会丢失文件属性所有者等）

gunzip file.bz：解压缩 （-d同）

-c：将文件显示出来（结果输出至标准输出，保留原文件不改变）

gzip -c m.txt >m.txt.gz :原文件不丢失需重定向

gzip -9 m ：-9为指定压缩比，值越大压缩比越大 

zcat file.gz：预览压缩包中的内容

bzip2 [option] file:压缩文件，压缩完成后原文件删除（比bz压缩比更高）

-k：原文件不删除

bunzip2 file.bz2：解开压缩包（-d同）

bzcat file.bz2：查看压缩包内内容

xz [option] file：压缩文件,压缩完成后原文件删除(压缩比 比bz2更高)

unxz file.xz：解压缩

-k：保留原文件

xzcat：查看压缩包内内容

以上压缩方式只对文件生效

zip -r 压缩生成文件  对某文件进行压缩：压缩目录，压缩比与gz类似（可压缩文件夹）

unzip file.zip：解压缩

打包：

tar 

c:创建归档

p：保留权限

v：查看过程

f：后跟文件或多个文件

r：追加文件进已成功的包内

t：查看包内文件列表

x：解包

z：打包操作后并压缩成为.gz后缀（解包无需添加）

j：同z后缀为.bz2（解包无需）

J：同z后缀后.xz（例：tar Jcvf，解包无需添加）

--exclude：排除

cpio [option] < file.cpio 解包格式

cpio [option] >file 打包格式（默认都在当前目录）

-o：打包

-i：解包

-d：解包生成目录  自动建立

sed：

sed [option] script inputfile

script:地址，命令

option：

-n:只打印操作的行

-i：直接修改文件而不是打印（-i.bak会将原文件添加.bak后缀并另存，可在使用此选项修改文件是做备份）

编辑命令：只在打印中，默认不修改文件

d：删除（只在显示中不是真正删除）

p：打印（默认及打印加p再次打印）

a：在指定行后面追加文本，支持使用\n实现多行追加 

i：在行前面插入

c：替换

w：匹配的行进行另存为

r：读取文件中的行到行后

=：为匹配的行打印行号

！：取反

s///：查找替换（如果替换行内多个字符默认只替换第一个）

g：全局替换

p：显示替换成功的行

'''$str''':sed特殊写法，调用变量时使用三引号

nl file ：显示行号空行不加
