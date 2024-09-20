💡**本章教程主要针对JMeter在windows 环境下进行api服务的压力测试**

### 一、 下载JMeter
1. 进入官网(https://jmeter.apache.org/download_jmeter.cgi) 下载JMeter工具压缩包 
![image](https://github.com/user-attachments/assets/6a5850f5-1ef7-4b2f-b751-99e37d803922)
![image](https://github.com/user-attachments/assets/a086462e-1e25-4d34-8312-db80e72327b7)

2. 本地安装openJdk环境，此处不详细阐述openJdk的安装流程，需要安装教程的可以前往(https://cloud.tencent.com/developer/article/2224916)
3. 将下载好的JMeter压缩包解压，启动JMeter前需要确定本地已经安装好openJDK，检查本地是否安装openJDK通过命令行输入java -version，如出现下图所示则表示已经安装成功。
![image](https://github.com/user-attachments/assets/6e7ab0be-ed4b-4cce-99df-8bfb15939147)

### 二、 运行JMeter
1. 从解压出来的文件夹中找到bin文件夹然后在bin文件夹里面找到 jmeter.bat，双击jmeter.bat等待JMeter启动。
![image](https://github.com/user-attachments/assets/5ca53eea-de7a-4bf5-86a5-14c5db176f04)
![image](https://github.com/user-attachments/assets/ff90d669-9a26-435a-aca4-a1097cea0f10)

2. 添加线程组
![image](https://github.com/user-attachments/assets/dbd9ad02-4f93-40c7-b7fa-4d2faae8a0f7)

3. 设置线程组参数
**Number of Threads (users)**：指虚拟用户数。默认为 1，则表明模拟一个虚拟用户访问被测系统。如果想模拟 100 个用户，则此处输入 100。
**Ramp-Up period (seconds)**: 虚拟用户增长时长。举个例子：比如你测试的是一个考勤系统，实际用户登录使用考勤系统的时候并不是大家一起登录。实际的使用场景可能是 9:00 上班，那么从 8:30 开始，考勤系统会陆陆续续有人开始登录，直到 9:10 左右。如果完全按照用户的使用场景来设计测试，此处应输入 40（分钟）* 60（秒）= 2400。但实际测试一般不会设置如此长的 Ramp-Up 时间，原因是你难道想要等上 40 分钟吗？一般情况下，可以估算出登录频率最高的时间长度，比如此处从 8:55 到 9:00 登录的人最多，那么这里设置为 60秒。如果“线程数”输入为 100，则意味着在 1 分钟内 100 个用户登录完毕。
**Loop Count**：循环次数。默认为 1，意味着一个虚拟用户做完一遍事情之后，该虚拟用户停止运行。如果选中“永远”，则意味着测试运行起来之后就根本停不下来了，除非手动停止。
4. 添加被测页面
- 添加被测API。
![image](https://github.com/user-attachments/assets/50f45da5-c9fa-4cba-9f3b-96c2ca3bfd1f)

- 设置请求参数。
![image](https://github.com/user-attachments/assets/c3f42c69-7c7d-4f77-8039-9639d0382b45)

- 为了方便测试可以将服务域名保存在用户定义的变量中（*Add —> Config Element —> User Defined Variables*）。
![image](https://github.com/user-attachments/assets/10c1f698-3887-486c-ad28-5cc6946a8ba8)

- 为了模拟多账户可以在被测页面中添加用户参数(*Add —> Pre Processors —> User Parameters*)。
![image](https://github.com/user-attachments/assets/3a5d730a-85dc-4fe7-9cd5-612adda15e9a)

- 为了正确请求被测页面可能需要带上请求头信息，可以使用HTTP信息头管理器(*Add —> Config Element —> HTTP Header Manager*)。
![image](https://github.com/user-attachments/assets/5359e0f9-3735-4734-95b3-7efa7d1a5ed9)

- 如果保存登录信息时使用到了Cookie，可以使用HTTP Cookie管理器(*Add —> Config Element —> HTTP Cookie Manager*)。
![image](https://github.com/user-attachments/assets/aeaf94c8-5aaf-41d3-aa52-a3063a1020b6)

- 为了方便查看结果可以被测页面添加查看结果树(*Add —> Listener —> View Results Tree*)。
![image](https://github.com/user-attachments/assets/301a001b-e3c4-437a-a36e-66a17d81e0cc)

5. 保存设置并运行
![image](https://github.com/user-attachments/assets/a84e793a-ef1b-4844-b886-5be5913b058d)

6. Demo 
这里提供登录的Demo设置参数，可以通过JMeter打开文件直接查看 [demo.jmx](https://github.com/witeem/Wiki/blob/main/JMeter/demo/demo.jmx)
