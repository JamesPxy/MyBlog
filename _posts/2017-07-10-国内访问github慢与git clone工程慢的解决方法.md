---
layout: post
title:  国内访问github慢与git clone工程慢的解决方法
date:   2017-7-10 10:59:00 +0800
categories: Android
tag: github
---
* content
{:toc}


1.    快速访问github网站

---

## 修改host文件配置，增加映射

```
-       浏览器访问IPAddress.com
- 
-       分别获得github.com和github.global.ssl.fastly.net对应的ip
- 
-       修改本地host
- 
-       打开Host文件   c:\windows\system32\drivers\etc
- 
-       增加host映射
```
    eg:
    	        151.101.44.249 global-ssl.fastly.Net
    		192.30.253.113 github.com

```
		
## -      更新DNS缓存

			刷新DNS缓存的方法一：

				首先进入命令提示符下（开始——运行——cmd）；

				先运行:ipconfig /displaydns这个命令,查看一下本机已经缓存了那些的dns信息的,然后输入下面的命令

				ipconfig /flushdns

				这时本机的dns缓存信息已经清空了,我们可以再次输入第一次输入的命令来看一下,

				ipconfig /displaydns

			刷新DNS缓存的方法二：

				直接禁用网卡再启用网卡，这样也可以
				
				

2.  **git clone快速**

-    git clone默认下载项目的完整历史版本，如果只关心代码的最新版则可以执行以下clone命令（ —depth==1 表示最新的版本，浅复制，数据量小）：
         
```
             git clone --depth=1 https://github.com/aaronshang/iOSPro.git
```

-   若想继续获取完整历史信息
        
```
            git fetch —unshallow
```
