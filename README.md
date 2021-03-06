[![Run on Repl.it](https://repl.it/badge/github/zhang0peter/bilibili-video-information-spider)](https://repl.it/github/zhang0peter/bilibili-video-information-spider)
## 声明
* 代码、教程均为本人原创，且仅限于学习交流，请勿用于任何商业用途！   
*******


我已经配置好项目在`Repl.it`上，你可以直接点击`Repl.it`的图标运行程序。

数据结果在最下面。            

## 准备工作

在2018年2月24，B站视频av号已经到2000万了，也就是说有2千万视频上传在了B站。

我使用的是Python3，数据库用的是Python自带的sqlite，使用requests库爬取。            
安装需要的库            

```python
pip install requests
```

直接刷新视频页面来获取视频信息太慢，通过api地址能快速获取视频信息。            
如：https://api.bilibili.com/x/web-interface/archive/stat?aid=19801429            
在浏览器中打开这个页面，可以获取json格式的数据：            
```javascript
{
  "code":0,
  "message":"0",
  "ttl":1,
  "data":{
    "aid":19801429,
    "view":583,
    "danmaku":4,
    "reply":2,
    "favorite":378,
    "coin":6,
    "share":6,
    "now_rank":0,
    "his_rank":0,
    "no_reprint":0,
    "copyright":2}
}
```
使用requests库获取数据，可以使用多线程爬虫进行加速，多线程的代码我不放出来。            

## 数据获取
B站对爬虫采取的是一旦发现，就封ip半小时到1天不等的时间。            
可以使用代理防封IP。            
我把爬虫放到服务器上跑了整整5天，获得了1300万条有效数据。数据库文件有300M，GitHub无法上传，            

## 数据处理
我使用的是SQLiteStudio进行数据库操作            
### 查询播放量前十的视频
![](image/查询播放量前十的视频.png)            
### 查询收藏数前十的视频
![](image/查询收藏数前十的视频.png)            
### aid号与播放量关系
可以从下图看出，随aid号的增加，视频的平均播放量在变少，爆款视频也在变少。            
我认为主要原因是B站UP主变多，把许多大的UP主的粉丝分流了部分。            
画图代码见 [aid号与播放量关系.py](code/aid号与播放量关系.py)            
![](image/aid号与播放量.png)            
### 收藏数与硬币数关系
画图代码见 [收藏数与硬币数关系.py](code/收藏数与硬币数关系.py)            
![](image/收藏数与硬币数关系.png)            
爬虫代码见 [bilibili-spider.py](bilibili-spider.py)            
参考资料： [bili-spider](https://github.com/chenjiandongx/bili-spider)            
