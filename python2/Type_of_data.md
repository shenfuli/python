# 二、Python 的基本数据类型 #

## 1、整数 ##

Python 可以处理任意大小的整数，当然包括负整数，在 Python 程序中，整数的表示方法和数学上的写法一模一样，例如：`1`，`100`，`-8080`，`0`，等等。

计算机由于使用二进制，所以，有时候用十六进制表示整数比较方便，十六进制用 0x 前缀和 0-9，a-f 表示，例如：0xff00，0xa5b4c3d2，等等。


## 2、浮点数 ##

浮点数也就是小数，之所以称为浮点数，是因为按照科学记数法表示时，一个浮点数的小数点位置是可变的。整数和浮点数在计算机内部存储的方式是不同的，整数运算永远是精确的（除法也是精确的），而浮点数运算则可能会有四舍五入的误差。

## 3、字符串 ##

字符串是以 '' 或 "" 括起来的任意文本，比如 `'abc'` ，`"123"` 等等。请注意，'' 或 "" 本身只是一种表示方式，不是字符串的一部分，因此，字符串 `'abc'` 只有 a，b，c 这 3 个字符。这个其他的编程语言也是类似的。


### （1） Python 中的字符串和字符串转义 ###

在上面那里提到，字符串可以用 `''` 或者 `""` 括起来表示。可是有些时候，我们字符串本身就包含了 `''` 或者 `""` ，怎么办呢？

那这个时候就需要对字符串的某些特殊字符进行“转义”，Python 字符串用 `\` 进行转义。跟 JAVA 也是一样的。

常用的转义字符还有：
``` 
\n 表示换行
\t 表示一个制表符
\\ 表示 \ 字符本身
```
具体例子：

![Python字符串转义.png](http://upload-images.jianshu.io/upload_images/2136918-88fdd2055dd834f4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

那上面就有一个问题呢，如果一个字符串包含很多需要转义的字符，对每一个字符都进行转义会很麻烦。这里为了应付这种情况，我们可以在字符串前面加个前缀 `r` ，表示这是一个 raw 字符串，里面的字符就不需要转义了。

![Python转义r.png](http://upload-images.jianshu.io/upload_images/2136918-8391230097f54800.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

但是，要注意的一点是，但是`r'...'`表示法不能表示多行字符串，也不能表示包含`'`和`"`的字符串。

如果要表示多行字符串，可以用`'''...'''`表示,当然你也还可以在多行字符串前面添加 `r` ，把这个多行字符串也变成一个raw字符串


![多行转义.png](http://upload-images.jianshu.io/upload_images/2136918-36df87f50895af18.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### （2） 字符串的编码问题 ###

我们都知道计算机只能处理数字，如果要处理文本，就必须先把文本转换为数字才能处理。最早的计算机在设计时采用8个比特（bit）作为一个字节（byte），所以，一个字节能表示的最大的整数就是255（二进制11111111=十进制255），0 - 255被用来表示大小写英文字母、数字和一些符号，这个编码表被称为ASCII编码，比如大写字母 A 的编码是 65，小写字母 z 的编码是 122。

如果要表示中文，显然一个字节是不够的，至少需要两个字节，而且还不能和 ASCII 编码冲突，所以，中国制定了 GB2312 编码，用来把中文编进去。

类似的，日文和韩文等其他语言也有这个问题。为了统一所有文字的编码，Unicode 应运而生。Unicode 把所有语言都统一到一套编码里，这样就不会再有乱码问题了。

Unicode 通常用两个字节表示一个字符，原有的英文编码从单字节变成双字节，只需要把高字节全部填为 0 就可以。

因为 Python 的诞生比 Unicode 标准发布的时间还要早，所以最早的Python 只支持 ASCII 编码，普通的字符串 'ABC' 在 Python 内部都是 ASCII 编码的。

Python 在后来添加了对 Unicode 的支持，以 Unicode 表示的字符串用`u'...'`表示。

不过在最新的 Python 3 版本中，字符串是以 Unicode 编码的，也就是说，Python 的字符串支持多语言。就像上面的例子一样，我的代码中没有加`u'...'`，也能正常显示。

不过由于 Python 源代码也是一个文本文件，所以，当你的源代码中包含中文的时候，在保存源代码时，就需要务必指定保存为 UTF-8 编码。当Python 解释器读取源代码时，为了让它按 UTF-8 编码读取，我们通常在文件开头写上这两行：

```python
#!/usr/bin/env python3
# -*- coding: utf-8 -*-
```

第一行注释是为了告诉 Linux/OS X 系统，这是一个 Python 可执行程序，Windows 系统会忽略这个注释；

第二行注释是为了告诉 Python 解释器，按照 UTF-8 编码读取源代码，否则，你在源代码中写的中文输出可能会有乱码。

申明了 UTF-8 编码并不意味着你的 .py 文件就是 UTF-8 编码的，必须并且要确保文本编辑器正在使用 UTF-8 without BOM 编码

## 4、布尔值 ##

布尔值和布尔代数的表示完全一致，一个布尔值只有 `True` 、 `False `两种值，要么是 `True`，要么是 `False`，在 Python 中，可以直接用 True、False 表示布尔值（请注意大小写），也可以通过布尔运算计算出来。

布尔值可以用 `and`、`or` 和 `not` 运算。

`and` 运算是与运算，只有所有都为 True，and 运算结果才是 True。

`or` 运算是或运算，只要其中有一个为 True，or 运算结果就是 True。

`not` 运算是非运算，它是一个单目运算符，把 True 变成 False，False 变成 True。


## 5、空值 ##

基本上每种编程语言都有自己的特殊值——空值，在 Python 中，用 None 来表示