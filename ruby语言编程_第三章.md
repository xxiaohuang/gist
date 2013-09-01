#第三章
##数据类型和对象

###3.1 数字
Ruby含有5个数字的内建类

![数值类继承关系](./ruby学习笔记/图片/3-1.jpg)

Ruby中所有数字对象都是Numeric类的实例。

所有的整数都是Integer类的实例。

如果一个整数值能容纳在31个二进制位里，它就是Fixnum类的实例，否则就是Bignum类的实例。他们之间是透明的转换。

Complex、BigDecimal、Rational类并非Ruby的内建类

Complex：复数

BigDecimal：具有任意精度的实数，使用的是__十进制表示法__。

Rational：有理数，即两个整数相除后得到的数。

###3.1.1 整数字面量

可以在整数字面量插入下划线（不在开头 也不在结尾），被称为千分符（thousands separator）

	1_000_000_000   # one billion(or 1,000 million in the UK)

0x/0X  : 十六进制

0b/0B  : 二进制

0      : 八进制

###3.1.2 浮点数字面量

Ruby要求在小数点的前后都要有数字出现。
必须写成 __0.1__， `.1`是错误的。2013/8/18 22:04:59 2013/8/18 22:05:00 2013/8/18 22:05:01 2013/8/18 22:05:02 2013/8/18 22:05:03 

###3.1.3 Ruby中的算术操作

除数为0的__整数__除法将导致一个 __ZeroDivisionError__ 被抛出。

除数为0的__浮点数__除法不会导致错误，只会返回一个名为 “Infinity”的值

0.0/0.0 是一个特例。它等于另一个特殊的浮点值，即NaN，表示 Not-a-Number。

 >Ruby采取的是向__负无穷大__圆整，但C及相关语言是向0圆整
 
取模操作符的定义也不同

 >Ruby中，始终和第二个操作数的符号保持一致，但在C和Java中，始终和第一个操作数的符号保持一致。
 >
 >Ruby还定义了一个remainder方法，在结果的量和符号方面，它的行为都类似于C的取模操作。

###3.2 文本

Ruby使用String类的对象表示文本。

 >有一些可支持一种字符串内插语法（string interpolation syntax），他可以将任意的Ruby表达式的值替换到字符串字面量中。
 
Ruby使用`Regexp`对象表示文本模式。

####3.2.1 字符串字面量

#####3.2.1.1 由单引号引用的字符串字面量
	'this is a simple Ruby string literal'

	'won\'t you read O\'Reilly\'s book?'

反斜线还可以转义另一个反斜线，这样第二个反斜线就不再是转义字符了。

	'This string literal ends with a single backslash: \\'
	'This is a backslash-quote:\\\''
	'Two backslashes:\\\\'

如果一个反斜线后面的字符不是单引号，也不是反斜线，那么这个反斜线就没有任何意义
	'a\b' == 'a\\b'

单引号引用的字符串可以跨越多行，得到的字符串字面量里包含换行字符。

	'this is a long string literal \
	that includes a backslash and a newline'

如果一个由单引号引用的长字符串分布到多行里而不引入换行符，只要简单地将其划分成彼此相邻的字符串字面量即可。

	message = 
	'These three literals are' \
	'concatenated into one by the interpreter. '\
	'The resulting string contains no newlines.'

####3.2.1.2 由双引号引用的字符串字面量

双引号 引用的字符串字面量支持许多转义序列，比如：

__换行__ ：  \n

__tab__ ：  \t

__双引号__： \"

	"\t \"This quote begins with a tab and ends with a newline \"\n"
	"\\" #A single backslash

>\u 这个转义序列能够将任意的Unicode字符嵌入由双引号引用的字符串里。

由双引号引用的字符串字面量可以包含任意的Ruby表达式。

这些表达式位于花括号中，且在花括号前面有一个#字符，此外整个结构位于由双引号引用的字符串中。

	"360 degrees=#{2*Math::PI} radians"    #"360 degrees =6.28318530717959 radians" 

当插入到字符串字面量中的表达式只是一个对于全局、实例或类变量的引用时，花括号可以被省略：

	$salutation ='hello'
	"#$salutation world"

当#字符后面是__{、$、@__时，它前面用一个反斜线来进行转义。

	"My phone #: 555-1234"
	"Use \# { to interpolate expressions}"

####3.2.1.3 Unicode 转义序列

由双引号引用的字符串可以包含任意的Unicode字符，在\u之后加上4个十六进制数字（字母可以是大写或小写），他们代表位于0000和FFFF之间的Unicode码点。
	"\u00D7"
	"\u20ac"

在后面加一个  `{`符号，然后接1到6个十六进制数字，最后再接一个`}`.花括号之间的数字可以是位于0和10FFFF之间的任何Unicode码点，且开头的零可以省略

	"\u{A5}"
	"\u{3C0}"
	"\u{10ffff}"

特殊用法
	
	money = "\u{20AC A3 A5}"  #=> "€£¥"
	money = "\u{20AC	20	A3	20	A5}"   #=>"€ £ ¥	

> 各组之间用一个空格或tab进行分隔，开始花括号之后或花括号之前不允许有空格。

####3.2.1.4 字符串字面量的分界符
__%q__开头的字符串字面量遵守__单引号__引用字符串的规则。

__%Q__开头的字符串字面量遵守__双引号__引用字符串的规则。

####3.2.1.5 Here document

以__<<__或__<<-__开头，后面紧跟一个用于指定结尾分界符的标识符或字符串，

	document = <<HERE
	this is a string literal.
	It has two lines and abruptly ends...
	HERE

	greeting = <<HERE + <<THERE + "World"
	Hello
	HERE
	There
	THERE

####3.2.1.6 反引号所引用的命令的执行

当使用反引号（__\`__），该文本被视作为一个由双引号引用的字符串字面量来处理。该文本的值将被传递给一个特殊的名为  __Kernel.`__的方法，该方法将该文本的值作为一个操作系统shell命令来执行。并且将该命令的输出作为字符串返回。

%x  代替反引号：

	%x[ls]

	if windows
		listcmd = 'dir'
	else
		listcmd = 'ls'
	end

	listing = `#{listcmd}`

	listing = Kernel.`(listcmd)

####3.2.1.7 字符串字面量和可变性

Ruby在每遇到一个字符串字面量时，他都会新建一个对象。如果你在一个循环体内包含了一个字面量，那么Ruby在每次迭代的时候都会创建一个新的对象。

	10.times {put "test".object_id}

结果

	20802528
	20802384
	20802264
	20802144
	20802000
	20801868
	20801736
	20801580
	20801460
	20801292
	=> 10


