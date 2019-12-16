
1. 浏览因特网资源

http://www.baidu.com/seasonal/index.html

1)url方案（http)告知web客户端怎么访问资源，使用http协议

2）服务器位置（www.baidu.com）,告知web客户端资源位于何处

3）资源路径（seasonal/index.html）说明请求的是服务器上哪个特定的本地资源，服务器磁盘上的位置

方案：//服务器位置/路径

2.url语法

1）方案--使用什么协议

2）主机和端口

对下层使用了tcp协议的http来说，默认端口80

3）用户名和密码

很多服务器要求输入用户名和密码，ftp服务器就是常见的一个

```
ftp://ftp.prep.ai.mit.edu/pub/gnu

ftp://anonymous@ftp.prep.ai.mit.edu/pub/gnu

ftp://anonymous:my_passwd@ftp.prep.ai.mit.edu/pub/gnu
```


4）路径

说明了资源位于服务器的什么地方

5）参数 ；

6）查询字符串 ？

7）片段 #

3.url快捷方式

1）相对url

一般都是绝对url,html页面中跳转可使用相对url

2) 自动扩展url
 
 主机名扩展和历史扩展
