## 记一次SFTP文件传输

## **什么是 SFTP ？**

在了解 [SFTP](https://linuxstory.org/tag/sftp/) 之前，我们先看看什么是 [FTP](https://linuxstory.org/tag/ftp/) 。[FTP](https://linuxstory.org/tag/ftp/)（ File Transfer Protocol ）[文件传输协议](https://linuxstory.org/tag/%e6%96%87%e4%bb%b6%e4%bc%a0%e8%be%93%e5%8d%8f%e8%ae%ae/)，是一种常用来在两终端系统之间传输文件的方法。

SFTP ，即 SSH [文件传输协议](https://linuxstory.org/tag/%e6%96%87%e4%bb%b6%e4%bc%a0%e8%be%93%e5%8d%8f%e8%ae%ae/)（ SSH File Transfer Protocol ），或者说是安全[文件传输协议](https://linuxstory.org/tag/%e6%96%87%e4%bb%b6%e4%bc%a0%e8%be%93%e5%8d%8f%e8%ae%ae/)（ Secure File Transfer Protocol ）。SFTP 是一个独立的 SSH 封装协议包，通过安全连接以相似的方式工作。它的优势在于可以利用安全的连接传输文件，还能遍历本地和远程系统上的文件系统。

在大多数情况下，优先选择 SFTP 而不是 FTP ，原因在于 SFTP 最基本的安全特性和能利用 SSH 连接的能力。FTP 是一种不安全的协议，应当只有在特定的情况下或者你信任的网络中使用。

虽然 SFTP 集成了很多图形工具，但是这一篇使用指南会演示如何使用交互式命令行界面来使用它。以下就是使用指南

### **如何使用 SFTP 连接**

![img](https://raw.githubusercontent.com/professorZhu/images/master/linux/20181227170228.jpg) 

protocol选择SFTP方式

输入用户名密码

![img](https://raw.githubusercontent.com/professorZhu/images/master/linux/1544445926576.png) 

输入put + 回车 弹出页面选择要上传的文件

![img](https://raw.githubusercontent.com/professorZhu/images/master/linux/1544446080094.png) 



![img](https://raw.githubusercontent.com/professorZhu/images/master/linux/1544492247662.png) 



PS：其他详细操作可以google查询