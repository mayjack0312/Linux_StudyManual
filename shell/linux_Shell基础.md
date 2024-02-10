# 一、Bash Shell基础
### 1.Bash Shell简单介绍
- 管理整个硬件的其实是核心（kernel），通常用户（user）都是以shell来与核心沟通。
- 什么是Shell？
![这里写图片描述](http://img.blog.csdn.net/20180305213607244?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1YmluMTk5MWxpdWJpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
我们通过shell与核心沟通，shell相当于用户和核心之间的桥梁。		
- 系统当前有多少Shells？可以检查一下/etc/shells文件。我们一般使用linux支持最广泛的bash。
- Bash的主要优点：
	- 命令记忆能力：可以记忆使用过的命令。只要在命令行按“上下键”，就可以找到前一个输入的命令。
	- 命令与文件补全功能：
	- 热键[Tab]可以帮助我们少打很多字，并且确定输入的数据是正确的。
		- [Tab]接在一串命令的第一个字的后面，则为命令补全；
		- [Tab]接在一串命令的第二个字以后，则为“文件补齐”。
		- 想知道环境中可执行的命令有几个，直接在bash的提示符后输入两个[Tab][Tab]，就能输出所有可执行的命令了。
		- 如果想要知道系统中所有以c开头的命令，则按下c[tab][tab]即可。
	- 命令别名（alias）设置功能：alias lm='ls -al' 自定义lm替换ls -al 命令。
	- Shell scripts的强大功能
- Bash Shell的内置命令：type
	
	- 为了方便shell的操作，bash已经“内置”了很多命令，如cd和umask等，都是内置在bash中的。如何知道一个命令是外部命令（其他非bash套件所提供的命令）还是内置在bash命令中的？下面介绍命令type:
	

	```
	type [-tpa] name
	不加任何参数：type会显示出name是外部命令还是bash内置的命令。
	-t：加入该参数，type会将name通过下面这些文字显示出它的意义：
		file：表示为外部命令
		alias：表示该命令为命令别名所设置的名称
		builtin：表示该命令为bash内置的命令功能
	-p：如果后面接的name为命令，会显示完整的文件名（外部命令）或显示为内置命令
	-a：在PATH变量定义的路径中，列出所有含有name的命令，包含alias。
	```
	
- 执行命令
	

	```
	command [-options] parameter1 parameter2
	 命令       选项      参数（1）    参数（2）
	 command为命令的名称，如改变路径的命令为cd
	 -options为加入参数的设置，如-h等
	 parameter1 parameter2为跟在option后面的参数，或者是command的参数。
	```
### 2.Shell的变量功能
- 前面我们提到，在任何地方执行ls，系统就是通过PATH变量里的内容所记录的路径顺序来搜索该命令。这是系统默认的变量的作用，如果是个人设置方面的应用，比如路径，使用变量，并将该变量定义写在最前面，后面相关的路径名称都以变量来替换，只需修改一行，就修改了整个脚本，很方便。
- 变量的获取与设置：echo、变量设置规则、unset
	使用echo命令可以获取变量，获取变量时，前面必须加上$。
	
	```
	echo $PATH
	echo ${PATH}
	```
- 设置或修改某个变量的内容
	规定：
	- 1.变量与变量内容以等号“=”来连接
	- 2.等号两边不能直接接空格符
	- 3.变量名称只能是英文字母与数字，但数字不能是开头字符
	- 4.若有空格符，可以使用双引号或单引号将变量内容结合起来。需要注意的是：双引号内的特殊字符可以保持变量特性，但单引号内的特殊字符会变成一般符号。
	- 5.必要时使用转义字符“\”将特殊字符（Enter,$,\,空格等）转义为一般字符。
	- 6.在一串命令中，还需要通过其他命令提供的信息，可以使用这样的方式 'commond'，注意不是单引号，是数字键1左边的那个按键。
	- 7.若变量为扩展变量内容，需要以双引号及 \$变量名称如  "$PATH":/home继续累加内容。
	- 8.若该变量需要在其他子程序中执行，则需要用export 使用变量变成环境变量，如“export PATH”。
	- 9.通常大写字母为系统默认变量，自行设置变量可以使用小写字母，便于判断。
	- 10.取消变量的方法为：“unset 变量名称”

	```
	echo $myname  这条命令执行完，没有任何数据，因为这个变量还未设置，是空的
	myname=VBird  这条命令执行完，会将变量myname的内容设置为VBird
	echo $myname  这条命令执行完，显示VBird。
	```
	

	```
	例一：设置变量name，内容为VBird
	name = VBird  错误，因为有空白
	name=VBird  OK

	例二：设置变量的内容为VBird's name
	name="VBird's name"  OK
	name=VBird\'s\ name  OK  采用反斜线（\）转义特殊字符，如单引号和空格键

	例三：在PATH变量中“累加”:/home/dmtsai/bin目录
	PATH=$PATH:/home/dmtsai/bin  OK
	PATH="$PATH":/home/dmtsai/bin  OK

	例四：要将name的内容多出“yes”
	name=$nameyes  NOT OK name的内容成了$nameyes这个变量
	正确的写法：
	name="$name"yes
	name=${name}yes

	例五：如何让刚刚设置的name=VBird可以用在下一个Shell程序中
	name=VBird
	bash         进入到子程序
	echo $name   并没有刚设置的内容
	exit         离开刚才设置的子程序
	export name  
	bash         进入到子程序
	echo $name   出现设置的值了
	exit         离开刚刚的子程序

	“子程序”：就是说在当前这个Shell的情况下，去启用另一个新的Shell，那个新的Shell就是子程序。
	一般状态下，父程序的自定义变量是无法在子程序内使用的。但是通过export将变量变成环境变量后，就能够在子程序下应用了。

	例六：取消刚刚设置的name这个变量的内容
	unset name
	```
### 3.环境变量的功能
- 环境变量可以帮助我们实现很多功能，包括家目录的修改、提示符显示、执行文件搜索的路径，等等。
- 一些环境变量的说明

	```
	例一：列出当前Shell环境下所有环境变量及内容
	env   
	```
	![这里写图片描述](http://img.blog.csdn.net/20180309121440996?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1YmluMTk5MWxpdWJpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)		
	- 环境变量LANG表示主语言环境，如我们要使用utf-8，可以LANG=utf-8
	- set命令：在bash环境下，其实还有一些很重要的变量，这些变量是在“shell环境下有效”，如果是在“子程序”中，这些变量值就会不同了。用set命令除了会将环境变量列出来之外，其他的自定义变量，以及所有的变量，都会列出来。
	- 一般来说，不论是否为环境变量，只要与当前Shell的操作接口有关的变量，通常都会被设置为大写字母。
	set
	![这里写图片描述](http://img.blog.csdn.net/20180309131240482?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1YmluMTk5MWxpdWJpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)	

	- \$(关于本地shell的PID)：这个变量表示“当前这个shell的进程号”。要想知道shell的PID（process ID），使用echo $$即可。
	- ？（上一个执行命令的回传码）：	当我们执行某些命令时，这些命令都会回传一个执行后的代码。一般来说，执行成功，则回传一个0值，如果执行过程错误，则返回错误代码（一个非零值）。		
	![这里写图片描述](http://img.blog.csdn.net/20180309132124516?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1YmluMTk5MWxpdWJpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)	

- 自定义变量转成环境变量：export
自定义变量与环境变量区别：主要在于是否可以被子程序所引用。
取得一个bash后，即得到了一个子程序，若再执行一次bash，将进入“子程序”。由于您已经进入该子程序，所有在父程序中自定义的变量将不存在，存在于子程序的，仅有“环境变量”。

	```
	export 变量
	将自定义的变量转换成环境变量
	
	export 后面没有跟变量，会把所有环境变量显示出来
	```
### 4.其他一些变量知识
- 语系文件的变量（locale）

	```
	locale -a
	会显示出linux支持的语系
	```
- 变量的有效范围
	- 启动一个shell时，操作系统分配一块内存给shell使用，这个区域的变量可以让子程序访问；
	- 利用export功能，可以让变量内容写到上述内存中（环境变量）；
	- 当加载另一个shell时（即启动子程序，离开原来的父程序），子shell可以将父shell的环境变量所在的内存导入自己的环境变量区块中。
	
- 变量键盘读取、数组与声明：read、array、declare
	- read(读取来自键盘输入的变量)
	

	```
	read [-pt] variable
	参数：
	-p：后面可以接提示符
	-t：后面可以接等待的“秒数”。
	```
![这里写图片描述](http://img.blog.csdn.net/20180309135533590?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1YmluMTk5MWxpdWJpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

	![这里写图片描述](http://img.blog.csdn.net/20180309135935646?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1YmluMTk5MWxpdWJpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
	- declare/typeset（声明变量的属性）
	如果declare后面没有任何参数，那么会将所有的变量名与内容都调出来，就像使用set一样。
	

	```
	declare [-aixr] variable
	参数：
	-a：将后面的variable定义为数组（array）
	-i：将后面的variable定义为整数数字（integer）
	-x：用法与export一样，将后面的variable变成环境变量
	-r：将一个variable变量设置成只读（readonly）该变量不可更改内容，也不能取消设置(unset)

	例：
	sum=100+300+500
	echo $sum  显示结果为100+300+500，因为这是文字类型的变量属性，不会求和
	declare -i sum=100+300+500
	echo $sum  显示结果为900
	```

	- 数组属性array的说明
	

	```
	var[index]=content
	有一个数组名为var，index为数字角标，这个数组的内容为var[1]=小明，var[2]=大明，...

	读取数组，以${数组}的方式来读取。
	```
- 与文件系统及程序的限制关系：ulimit
假如有10个人同时登陆了一台Linux主机，这10个人同时打开了100个文件，每个文件的大小约10MB，Linux的内存需要10*100*10=10000MB，这样显然会造成系统死机。为了预防这种情况的发生，我们可以通过ulimit限制可打开的文件数量、可以使用的CPU情况、可以使用的内存总量。

	```
	ulimit [-SHacdflmnpstuv] [配额]
	参数：
	-H：hard limit，严格设置，必定不能超过设置的值
	-S：soft limit，警告设置，可以超过这个设置值，但会有警告，
	-a：列出所有的限制额度
	-f：此shell可以建立的最大文件容量，单位为KB
	其他参数用到时再查
	```
- 附加的变量设置功能

	```
	echo $HOME
	echo ${HOME} 这种方法中，我们可以修改变量。只要加上一些字符标志，后面再接着使用比较字符串，就能修改变量的内容了。

	例：以vbird="/home/vbird/testing/testing.x.sh"为例
	1. 在vbird变量中，从最前面开始比较，若开头为/，则删除两个/之间所有的数据，即/*/
	echo ${vbird##/*/} 
	结果：testing.x.sh
	echo ${vbird#/*/}  
	结果：vbird/testing/testing.x.sh      ##表示去后面字符串最长的那一段；#表示取最小的那一段
	
	2.从后面开始删除，删除/*?
	echo ${vbird%%/*/}
	结果：删除失败
	echo ${vbird%%/*}
	结果：/home/vbird/testing
	%%/*表示删除最长的那一段，%/*表示删除最短的一段

	3.将vbird变量中的testing替换为TEST
	echo ${vbird/testing/TEST}
	结果：/home/vbird/TEST/testing.x.sh
	echo ${vbird//testing/TEST}
	结果：/home/vbird/TEST/TEST.x.sh
	如果后面接/，表示后面进行的是替换工作，而且仅替换第一个
	如果是//，则表示替换全部字符串。
	```

### 5.命名别名与历史命令
- 命令别名设置：alias、unalias

	```
	如果要查询隐藏文件，并且需要列出很长的信息，要一页一页地翻看，则需要执行“ls -al|more”
命令，可以使用lm简化
	alias lm='ls -l | more'

	取消别名的设置
	unalias lm
	```
- 历史命令：history

	```
	history [n]
	history [-c]
	history [-raw] histfiles

	参数：
	什么都不接，默认输出当前内存的所有历史记忆
	n：数字，表示列出最近的n行命令
	-c：将当前shell中所有的history内容全部清除
	-a：将当前新增的history命令加入到histfiles中，若没有加入histfiles，则默认写入~/.bash_history
	-r：将histfiles的内容读取到当前shell的历史记忆
	-w：将当前的历史记忆内容写入histfiles中
	```
### 6.管道命令（pipe）
- bash 命令执行时，会出现数据。如果这组数据必须经过几道手续之后才能得到所想要的格式，如何设置？这可以通过管道命令完成，管道命令使用 | 这个分隔符。
	
	![这里写图片描述](http://img.blog.csdn.net/20180309162036125?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1YmluMTk5MWxpdWJpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
	管道命令"|"仅能处理通过前面一个命令传来的正确信息，也就是标准输出（STDOUT）的信息，对于标准错误，并没有直接处理的能力。下面介绍一下基本的管道命令。

- 选取命令：cut、grep

	```
	这个命令可以将一段消息的某段“切”出来。处理的消息是以“行”为单位。
	cut -d '分隔符' -f fields
	参数：
	-d：后面接分隔符。与-f一起使用。
	-f：根据-d的分隔符将一段消息分为数段，用 -f 取出第几段的意思。
	
	例：
	echo $PATH | cut -d ':' -f 5   将PATH变量用“:”切割成几段，取出第5段
	echo $PATH | cut -d ':' -f 3,5   将PATH变量用“:”切割成几段，取出第3段和第5段

	cut -c 字符范围
	参数：
	-c：以字符为单位（characters）为单位取出固定的字符范围

	例：
	export | cut -c 12-  将export输出的消息，取得第12个字符以后的所有字符串
	```

	```
	cut是将一行消息中取出我们想要的部分，grep则分析一行消息，若其中有所需要的信息，就将该行取出。
	grep [-acinv] '搜索字符串' filename
	参数：
	-a：将二进制文件以文本的方式搜索数据
	-c：计算找到‘搜索字符串’的次数
	-i：忽略大小写的不同，所有大小写视为相同
	-n：顺便输出行号
	-v：反向选择，即显示出没有 '搜索字符串' 内容的那一行

	last | grep  'root'   将last中出现root的一行取出来
	last | grep -v 'root'   只要没有root的就取出
	last | grep  'root' | cut -d ' ' -f 1   在last的输出消息中，只要有root就取出，并且仅取出第一栏
	```
- 其他命令（命令较多，就不做具体介绍了）
	- 排序命令：sort、wc、uniq
	- 双向重导向：tee
	- 字符转换命令：tr,col,join,paste,expand
	- 拆分命令：split

# 二、正则表达式（请参考鸟哥的Linux私房菜）
	
# 三、Shell脚本
### 1.shell脚本基本介绍
- 什么是shell脚本？
	shell脚本是利用shell功能所编写的“程序（program）”，这个程序使用纯文本文件，将一些shell的语法与命令写在里面，与正则表达式、管道命令与数据流重导向一起实现我们的目的。
- 为什么学习shell脚本？
	- 自动化管理的重要依据
	- 追踪与管理系统的重要工作
	- 简单的入侵检测功能
	- 连续命令单一化
	- 简单的数据处理
	- 跨平台支持与缩短学习历程
### 2.第一个脚本的编写与执行
- shell脚本其实就是纯文本文件（ASCII），我们可以编辑这个文件，然后让这个文件帮我们一次执行多个命令。编写shell脚本时需要注意的事项：
	- 命令与参数间的多个空白会被忽略掉。	
	- 如果读到一个ENTER符，就开始执行该命令。
	- 如果一行内容太多，则可以使用\[Enter]来扩展至下一行。
	- 此外，#可作为注释。任何加在#后面的内容，将会被视为注释文字而被忽略。
- 假设我们编写好的文件名是shell.sh，如何执行该文件？
	- 将shell.sh加上可读与执行（rx）权限，然后就能用./shell.sh来执行了。
	- 或者使用sh shell.sh的方式来直接执行即可。
- 编写第一个脚本

	![这里写图片描述](http://img.blog.csdn.net/20180310144632459?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1YmluMTk5MWxpdWJpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
	- 1.!#bin/bash在声明这个脚本使用的shell名称：因为使用的是bash，所有必须要用“!#bin/bash”来声明这个文件内的语法使用bash的语法。当执行这个程序时，它就能加载bash的相关环境设置文件，并且执行bash来使下面的命令执行。这一行很重要，因为如果没有的话系统很可能无法判断要使用声明shell来执行。
	- 2.#后面的是注释
	- 3.主要环境变量的声明：建议将重要的环境变量设置好。PATH变量比较重要，设置好PATH，可让程序在进行时，直接执行命令，而不必写绝对路径。
	- 4.主要程序部分：将主要的程序写好。
	- 5.告知执行结果：可以使用exit命令让程序中断，并给系统回传一个数值0。
	
	执行结果：
	![这里写图片描述](http://img.blog.csdn.net/20180310151947626?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1YmluMTk5MWxpdWJpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### 3.简单的Shell脚本练习
- 变量内容由用户决定
	

	```
	编写一个脚本，让用户输入名字，然后在屏幕上打印用户名字
	#!/bin/bash
	#Program: this is a practice
	PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
	export PATH
	
	read -p "Please input your name:" name
	echo -e "your name is : $name"
	```
- 利用date建立文件

	```
	#!/bin/bash
	#Program: this is a practice
	PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
	export PATH

	1.让用户输入文件名，并获取fileuser变量
	read -p "Please input the filename what you want:"fileuser
	
	2.为了避免用户随意按ENTER，使用变量功能分析是否设置了文件名？
	filename=${fileuser:-"filename"}

	3.开始使用date命令来获取所需要的文件名
	date=`date --date='2 days ago' +%Y%m%d'
	file="$filename""$date"

	4.建立文件名
	touch $file
	```
- 数值运算的方法

	```
	#!/bin/bash
	#Program: this is a practice
	PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
	export PATH

	read -p "first number:" firstnum
	read -p "second number:" secondnum

	total=$(($firstnum*$secondnum))
	echo -e "the total is: $total"
	```
	数学运算可以使用“declare -i total=\$firstNum*\$secondNum”，但建议使用上面的方式进行。
    var=$((运算内容))，不仅容易记忆，而且更加方便。

### 4.善用判断条件
- 使用test命令的测试功能

	```
	test -e /dmtsai   检查/dmtsai是否存在
	执行结果不会显示任何消息，但最后可通过$?或&&及||来展现整个结果

	test -e /dmtsai && echo "exist" || echo "Not exist"  最后结果可以告诉我们是“exist”还是“Not exist”。
	```
- 测试标志

	```
	1.某个文件名的“类型”检测，如test -e filename
	-e：该“文件名” 是否存在
	-f：该“文件名” 是否为文件（file）
	-d：该“文件名” 是否为目录（directory）

	2.文件的权限检测，如test -r filename
	-r：检测该文件名是否具有“可读”属性
	-w：检测该文件名是否具有“可写”属性
	-x：检测该文件名是否具有“可执行”属性

	3.多重条件判断，如test -r filename -a -x filename
	-a：（and）两个条件同时成立
	-o：（or）两个条件任何一个成立

	还有比较两个文件、两个整数之间的判断、判断字符串的数据等，用到时再查询 
	```
- 使用判断符号[ ]
	除了使用test外，还可以使用判断符号[]来进行数据的判断。
	

	```
	判断$HOME变量是否为空
	[ -z "$HOME" ]    需要注意的是：上述每个组件中间，都要用空格符分隔

	判断两个字符串$HOME和$MAIL是否相同
	[ "$HOME" == "$MAIL" ]

	中括号内的变量，最好使用双引号来设置
	name="VBird Tsai"
	[ $name == "VBird" ]  
	结果会报错，因为$name没有用双引号括起来，那么上面的判断条件会变成：
	[ VBird Tsai == "VBird" ] 而不是我们要的  [ "VBird Tsai" == "VBird" ] 
	
	```
- Shell脚本的默认变量(\$0,\$1...)


### 5.条件判断
- if  then

	```
	语法：
	if [ 条件判断表达式 ]; then
		当条件表达式成立时，可以执行的命令
	fi

	当有多个条件需要判断时，除了将多个条件写入一个中括号，
	还可以使用多个中括号来隔开，而括号与括号之间，则以&&或||来隔开，他们的含义是：
	&&表示AND
	||表示or

	if [ 条件判断表达式 ]; then
		当条件表达式成立时，可以执行的命令
	else
		当条件表达式不成立时，可以执行的命令
	fi

	if [ 条件判断表达式一]; then
		当条件表达式成立时，可以执行的命令
	elif [ 条件判断表达式二]; then
		当条件表达式二成立时，可以执行的命令
	else
		当条件表达式一与二都不成立时，可以执行的命令
	fi
	```
- netstat
	该命令可以查询当前主机是否有打开的网络服务端口（service ports）
	部分网络服务
	![这里写图片描述](http://img.blog.csdn.net/20180310210533602?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvbGl1YmluMTk5MWxpdWJpbg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)
	常见的端口与相关网络服务的关系是：
	- 80：WWW
	- 22：ssh
	- 21：ftp
	- 25：mail
	

	```
	#!/bin/bash
	#Program: Using netstat and grep to detect WWW,SSH,FTP and Mail services
	PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
	export PATH

	testing=`netstat -tuln | grep ":80 "`
	if [ "$testing" != "" ]; then
		echo "WWW is running in your system."
	fi
	testing=`netstat -tuln | grep ":22 "`
	if [ "$testing" != "" ]; then
		echo "SSH is running in your system."
	fi
	testing=`netstat -tuln | grep ":21 "`
	if [ "$testing" != "" ]; then
		echo "FTP is running in your system."
	fi
	testing=`netstat -tuln | grep ":25 "`
	if [ "$testing" != "" ]; then
		echo "Mail is running in your system."
	fi
	```
- 使用case  esac判断

	```
	case $变量名称 in 
		"第一个变量内容")
		程序段
		;;
		"第二个变量内容")
		程序段
		;;
		*)
			不包含第一个变量内容与第二个变量内容的其他程序执行段
			exit 1
			;;
	esac
	```
	

	```
	#!/bin/bash
	#Program: Show "Hello" from $1 ... by using case ...esac
	PATH=/bin:/sbin:/usr/bin:/usr/sbin:/usr/local/bin:/usr/local/sbin:~/bin
	export PATH

	case $1 in
		"hello")
			echo "Hello,how are you?"
			;;
		"")
			echo "You MUST input parameters,ex>$0 some word"
			;;
		*)
			echo "Usage $0 {hello}
			;;
	esac

	假设上面的脚本文件名字为sh08.sh
	如果输入sh sh08.sh test执行，那么屏幕上就会出现“Usage sh08.sh{hello}”
	```
### 6.循环
- while do done、until do done

	```
	while [ condition ] 
	do
		程序段落
	done

	until [ condition ] 
	do
		程序段落
	done
	这种方式与while相反，它说的是当condition条件成立时，就终止循环，否则就持续执行循环的程序段。
	```
- for...do...done
相对于while、until的循环方式是必须要符合某个条件的状态，for这种语法是已经知道要进行几次循环的状态。
	
	```
	for(( 初始值; 限制值; 执行步长))
	do
		程序段
	done
	```