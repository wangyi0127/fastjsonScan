#### 更新了，注意升级！！更新到v3.8.1
 支持<=1.2.47的不出网检测方案！！！！其中有SpringEcho方案,TomcatEcho方案，有DelayTest方案。不出网利用链有3条:dbcp,ibatis和TemplatesImpl，其中TemplatesImpl几乎遇不到，但是也加着。正在研究一键写文件和内存马，后面更新可能会加入。

## fastjsonScan
fastjson漏洞burp插件，检测fastjson&lt;=1.2.47基于dnslog和fastjson 1.2.47 的不出网3种TomcatEcho,SpringEcho回显方案，使用ysoserial的tomcatEcho回显方案

附带fastjson1.2.47.tar.gz的web，解压到tomcat 的webapps，和fastjson 1.2.24的jar包，替换1.2.47的jar就能测试1.2.24。


   
#### FastjsonScan 更新
 1. 在原来的被动扫描上支持主动扫描，由于主动扫描发送数据包较多，故会多次扫描。
 2. 在原来的rmi协议上支持ldap协议。
 3. 支持fastjson 1.2.47 回显 ,检测后，发送到Repeater 中，便可以利用。
 4. 支持fastjson<= 1.2.47 的延时检测。
  ##### 4. 存在攻击行为，非法使用后果自负！！！！
 5. 为防止被动检测多次扫描，同一url被动检测一次，如果重新检测，需要重新加载插件或重启burp，主动扫描可以检测多次，目前主动扫描不会tomcatEcho和SpringEcho。
 ##### 6. 加入1.2.47-1.2.68 dnslog检测方案，高于1.2.47的利用条件苛刻。
 
#### 用法：
  加到burp插件就行了，流量经过burp就检测。结果在ISSUES中看到，如果<=fastjson 1.2.7的话，自动发送结果到Repeater如下图。
#### FastjsonExploit.jar
  打包大佬的代码，大佬地址：https://github.com/c0ny1/FastjsonExploit
  
#### 注意：
   只检测post，且类型是application/json
 
##### 如下图：
检测结果ISSUES中看到：

![](%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20210119112911.png)

fastjson1.2.47回显存在的话，自动发到Repeater 回显结果，添加Testcmd头执行命令：

![](%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20210118170804.png)

一键反弹shell：
![](%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20210118174907.png)

加入第二种回显方案：
也是自动检测，存在的话会发送到repeater中，如图，修改echo:test和Testcmd:命令：
![](微信截图_20210402211015.png)

第三种回显方案：
自动检测后，发送到repeater种，修改header，加入Testcmd:命令
![](微信截图_20210430091909.png)

#### 将要更新提示，后面打算加入内存马和webshell上传功能，还没实现，只弄了个界面：
![](微信截图_20210430141513.png)
