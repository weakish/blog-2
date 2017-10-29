---
title: 编码：二进制的世界
tags:
  - 科普
permalink: encoding-to-binary
date: 2015-11-21
---

我们要聊的编码并不是「写代码（Coding）」，而是信息从一种形式被转换为另外一种形式的这个过程，即 Encoding.

### 二进制的世界

就像大家知道的那样，在计算机的世界中，信息必须被转换为二进制（Binary）才能被 CPU 计算、被内存或硬盘存储、在网络上传输。

相比于我们从小使用的十进制，二进制既不直观，又显得冗长，那么为什么计算机选择二进制作为内部的信息表现形式呢？

十进制意味着每个数位上有从 0 到 9 十种可能的状态，也就是十进制中的一位可以表示 10 种事物中的一种，两位则可以表示 100 种事物的一种。要不是人有十个手指，其实我们也可以使用八进制（偶尔会在计算机领域使用）或十二进制（时间和角度通常基于十二进制）。

那么我们可以考虑一下极端情况，最少可以用几进制来表示信息呢？很好猜到答案 —— 二进制，要表达一个有意义的信息，至少要能区分两种的情况中的一种吧。科学家喜欢追求一种「简洁之美」，既然我们找到了表示信息的最简形式，为什么不以它为基础来构筑计算机世界呢。

这种「信息的最小单位」被称为比特 （Bit），正因为它是信息的最小单位，比特位之间的运算规则也远比十进制简单得多（例如两个比特位相加只有 4 种情况）；在工程上也得到了很多便利，例如比特的两种状态刚好被映射到信号的有无、低电压或高电压、连通或断开等等。

### 数字的编码

因为计算机选择了用比特作为信息的表现形式，所以各种其他的形式的信息必须被以某种方式被转换为若干个比特才能被计算机处理，这种过程就叫「编码」。

我们先从数字说起，数字是最容易被编码的信息了，因为比特可以被简单地看作二进制的数字，只需将我们平常的十进制数字换算到二进制即可。

在这种编码方式下，一个数字所需要的比特数正比于它的大小，比如用二进制表示 123 需要 7 个比特，而表示一亿则需要 27 个比特。使用这种方式编码数字存在一些局限性，例如需要大量的比特去表示一个较大的数、无法去表示小数点等。

所以还存在另一种被普遍使用的方法来编码数字，被称为「浮点数（Floating Point Number）表示法」。这种表示方法非常类似于「科学计数法」，它将一个数字拆分为三个部分来保存：正/负、指数、系数。这样的话，浮点数表示法可以在一个非常大的范围（受限于指数部分的位数）内表示包括小数在内的，具有一定精度（受限于系数部分的位数）数字。

### 字符串的编码

计算机中的「字符串（String）」就是人们通常所说的文字，一个字符串是由若干的「字符（Character）」构成的。而字符则取决于具体的语言，例如英语中的字符包括 26 个英文字母，而汉字则有两万余个字符。

计算机如何编码字符呢？储存它的图形显然会令问题复杂化，所以最简单的办法就是给每个字符一个编号，在计算机中储存和计算编号，直到需要展示的时候才绘制为人们所见到的图形。

最简单的一种字符编码方案就是 ASCII 了，它支持 128 个字符，包括大写和小写的 26 个英文字母、数字、英文标点和一些特殊字符。ASCII 将一个字符编码为 8 个比特，但实际只用到了 7 个比特而已（128 刚好是 2 的 7 次方）。

### 字符集和字符编码

为了对各种语言的字符提供支持，后来又出现了很多种将字符编号的规则，这种规则被称为「字符集（Character Set）」，例如中国官方最新的字符集标准被称为 GB18030, 包括了七万多个汉字和一些少数民族的字符。

字符集之间可能互不兼容，例如同样的一个二进制序列，在一个中文字符集中可能是一个汉字，而在其他的字符集中就可能是另外的字符，甚至是无法显示的字符。所以计算机在显示一段字符串的时候需要知道它的字符集，否则就会出现我们称之为「乱码」的情况，即字符串被以一种错误的字符集被显示，以至于无法阅读。

通常一段字符串只能使用一种字符集，一旦你选择了一种字符集，你就没有办法表示不在这个字符集中的字符。例如如果你选择了一个中文字符集，那么可能就没办法去表示韩文中的字符。为了解决这种不便，出现了一种叫「Unicode（暂译作通用字符集）」的字符集，它覆盖了世界上绝大部分语言的字符，甚至包括了经常被使用的表情符号（Emoji）。目前大部分的网页、编程语言、操作系统都使用 Unicode 来表示字符串。

和其他一些直接规定了编码方式的字符集不同，Unicode 本身只是对字符的编号，它定义了几种具体的编码方式。例如 UTF-8 最少使用 8 个比特，最多使用 48 个比特来表示一个字符，适合英文居多的场景（因为 ASCII 中的字符只需要 8 比特）；UTF-32 则总是用 32 个比特表示一个字符，这样固定长度的编码方式会拥有更好的性能。

### 来自自然界的信息

计算机经常还被用来处理图片、音频、视频这类来自自然界的信息。我们所生活在的物理世界可以被认为是「连续」的。例如自然界中的声音，在任意一个时间点都可能会有频率和响度的变化，但在目前的计算机体系来看，这样的数据拥有无限大的信息量，没办法被编码。

于是我们使用「采样」的方式将这些信息转化为有限的「离散」的信息。例如我们每一毫秒去测量声音的频率，这样计算机就可以去编码每次测量到的频率的数字，将这段声音数字化了。

这种采样的过程是会丢失信息的，比如在两次测量之间的某一时间点的情况我们是不得而知的，只能推测它大概介于这两次结果之间。所以很好想象，丢失的信息取决于采样的频率，以越短的间隔采样，就会得到越多的信息，越接近原始的信息。

未完待续，下一篇将会介绍更多有关「编码」的内容。