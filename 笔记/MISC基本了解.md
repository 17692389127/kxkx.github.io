# MISC

## 一、Recon信息搜集

获取信息的渠道，用百度，谷歌等方式搜索引擎的技巧

## 二、Encode编码转换

### 通信领域：

电话拨号编码：1-9使用1-9个脉冲，0使用10个脉冲

Morse(摩尔斯编码)，特点：只有.和_,最多六位，也可以用01串表示

敲击码：基于5*5的方格实现，K被整合到C中

曼彻斯特编码：位中间电平，从低到高跳变表示“1”，从高到低跳变表示“0”

用10表示二进制中的0，用01表示二进制中的1

优点：抗干扰，一般用于信道运输，缺点：效率低

格雷编码：所有相邻数据的二进制编码只有一位不同

###   计算机相关编码：

#### ASCII特点

采用可见字符，主要如下

0-9，48-57

A-Z，65-90

a-z,97-122

变形：二进制、十六进制编码：将ASCII转变为二进制和十六进制

Base编码：Basexx编码中的xx是采用多少个字符进行编码，比如说Base64就是采用64个字符进行编码。

#### base64编码

使用6个二进制位表示一个字符，可以表示64个不同的字符，包括26个大写字母，26个小写字母，10个数字，加号和斜线

编码原理1.将要编码的字符串转变为二进制

2.将二进制的字符串按照每六位一组进行分组，如果最后一组二进制不足六位的话，需要用0进行补位

3.将每组的二进制位转换成十进制的数字，到base64编码表中找到对应的字符，编码后的位数需要是4的倍数，如果不是，则需要用等号进行补齐



