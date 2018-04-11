# ProxySpider

代理爬虫请求框架是一个将网络代理IP和网络请求结合在一起的项目。主要分为两个部分一个部分是代理IP的爬取，一个部分是网络请求。
项目借鉴了开源的IP代理爬虫框架https://github.com/xiaosimao/IP_POOL
并对框架进行BUG修复和拓展。

本项目的特点：

1.支持Python3

2.对借鉴的IP代理爬虫框架进行了部分BUG修改和源码改动

3.将网络请求和IP代理结合，使用时只需要直接请求目的IP即可。

4.代理IP保存在MongoDB数据库中

5.支持自定义超时请求超时时间、代理超时时间、请求头设置、被目标网站屏蔽页面过滤、程序休息时间

6.网络请求过程中，IP失效时自动更替。

7.若代理IP集合全部失效，程序会进行阻塞休息然后更新并检测数据库中的代理IP

8.详细的日志信息，帮助及时了解请求情况


**欢迎star和使用这个github项目，也欢迎提各种issue和与我交流。**


## 使用方法
只需引入请求类，然后输入目标网站，设置是否使用代理即可请求。
![](https://github.com/yukunqi/ProxySpider/blob/master/%E4%BD%BF%E7%94%A8%E6%88%AA%E5%9B%BE.jpg)


## 文件介绍

整个项目分为两个部分，一个部分由ip_spider和ip_proxy组成，它们负责代理IP的抓取和维护工作。 main文件的部分则是进行使用者抓取目标网站
的请求类函数，通过前面部分抓取得到的IP来进行爬虫抓取操作。

### ip_spider
data_save.py 是用来将获取的IP插入数据库的

html_parser 负责解析代理IP网址

log_format 是日志对象的设置

page_downloader 是负责请求代理IP网址的方法，里面设置了请求的详细过程和参数

threads 负责多线程处理爬取代理IP的任务

tools 通用的工具方法

UAS 则是自定义的爬虫请求头部，用来模拟真实的浏览器请求


### ip_proxy
_request 用来检测代理IP是否失效

db_method 和代理IP相关的一些数据库操作

delete_not_update 是用于检测并更新数据库中存量的代理IP

proxy_basic_config 定义了JSON格式的代理IP网站的列表，里面可以自定义抓取的页数　请求的方法　地址等

work_spider 则是启动抓取代理IP程序的入口

### main文件

config 主要是网络请求的具体设置
mainRequest 是具体进行网络请求的主类
