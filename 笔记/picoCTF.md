# picoCTF

## Forensics

### DISKO1

使用strings命令查看文本，在其中查找关键词picoCTF得到flag

`strings disko-1.dd | grep 'flag'`

![](C:\Users\H2745\Pictures\Screenshots\屏幕截图 2025-05-28 151036.png)

### RED

用记事本打开图片后，发现出现了一首诗，诗的每行首字母都大写，提示查看LSB

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 152036.png)

使用zsteg -a命令，查看文件的LSB

`zsteg -a 'red (2).png'`

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 152424.png)

发现其中有一段base64编码，解码后得到flag

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 151904.png)

### Ph4nt0m 1ntrud3r

打开文件后，发现有几列base64码，使用strings命令提取文本然后解码，发现其中有flag碎片，但排序混乱



![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 153118.png)

查看题目提示，时间很重要，推测按时间排序，依次解码得到flag

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 153302.png)

picoCTF{1t_w4snt_th4t_34sy_tbh_4r_d4b57909}

### Verify

使用ssh远程连接，使用cat命令首先查看指定文件的内容

打开目录，遍历查看其中文件的哈希值

![image-20250528202730250](C:\Users\H2745\Desktop\笔记\picoCTF\image-20250528202730250.png)

在其中查找与源文件内容相同的文件，得到flag



![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 202814.png)

### Scan Surprise

打开压缩包后得到二维码图片，扫码即得flag

### Secret of the Polyglot

打开pdf文件，得到flag的一部分

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 203128.png)



1n_pn9_&_pdf_90974127}

将文件拖进010editor中，发现是PNG格式

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 203750.png)

将扩展名改为png,得到前半部分flag

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 203953.png)

### CanYouSee

用010editor打开图片，发现一段字符像base64编码，解码后得到flag

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 205859.png)

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 210036.png)

### information

使用exiftool命令查看图片详情，发现一串base64编码后的字符串，解码后得到flag

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 210520.png)

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 210307.png)

### Glory of the Garden

在记事本中打开，查找关键字，得到flag

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 210741.png)

### What Lies Within

LSB：使用zsteg命令

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 214011.png)

### extensions

打开txt文件，发现是PNG文件的文件头，更改扩展名为PNG,得到flag

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 214623.png)

### shark on wire 1

追踪流到第六个，得到flag

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 214908.png)

### So Meta

用记事本打开图片，搜索pico，得到flag

![](C:\Users\H2745\Desktop\笔记\picoCTF\屏幕截图 2025-05-28 215129.png)