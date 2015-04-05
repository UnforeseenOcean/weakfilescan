# weakfilescan
一款基于爬虫，动态收集扫描目标相关信息后，根据目标信息进行二次整理形成字典规则引擎，利用动态规则的多线程敏感信息泄露检测工具，该工具支持多种个性化定制选项，包括：
* 规则字典多样化定义（支持正则）
* 扫描域名策略（和域名全称相关, 和主域名相关, 和域名的名字相关）
* 自定义HTTP状态码
* 支持动态配置HTTP脚本扩展名
* 自定义判断文件是否存在正则
* 返回结果集误报清洗选项
* HTTPS服务器证书校验
* 线程数定义
* HTTP请求超时时间
* 是否允许URL重定向
* 是否开启Session支持，在发出的所有请求之间保持cookies
* 是否允许随机User-Agent
* 是否允许随机X-Forwarded-For
* 动态代理列表配置（支持TOR）
* HTTP头自定义

更多使用详情参照 [/config.py](https://github.com/ring04h/weakfilescan/blob/master/config.py)

# 快速开始
```
[root@localhost weakfilescan]# python wyspider.py http://wuyun.org php
{
  "dirs": {
    "http://wuyun.org": [
      "http://wuyun.org"
    ]
  }, 
  "files": {
    "http://wuyun.org": [
      "http://wuyun.org/wuyun.tar.gz"
    ]
  }
}
```

# 字典支持规则
## 规则使用简介

| 类型      |    说明 |
| :-------- |:--------|
| date | 日期 |
| int  | 整数 |
| str  | 字符 |
| re   | 正则引擎 |

### 日期类规则
| 类型      | 使用实例 |
| :-------- |:--------|
| 年 | {date=year:2010-2015}$ |
```
[2010,2011,2012,2013,2014,2015]
```
| 类型      | 使用实例 |
| :-------- |:--------|
| 月 | {date=mon:1-12}$ |
```
[1,01,2,02,3,03...9,09]
```
| 类型      | 使用实例 |
| :-------- |:--------|
| 日 | {date=day:1-31}$ |
```
[1,01,2,02,3,03,4,04,5,05...31]
```
| 类型      | 使用实例 |
| :-------- |:--------|
| 年月 | {date=year_mon:201501-201504}$ |
```
[201501,20151,201502,20152...201504]
```
| 类型      | 使用实例 |
| :-------- |:--------|
| 月日 | {date=mon_day:0501-0531}$ |
```
[0501，51，0502，52，0506,56,0511，511...0530,530]
```
| 类型      | 使用实例 |
| :-------- |:--------|
| 年月日 | {date=year_mon_day:20150101-20150401}$ |
```
[20150101,201511,20150112,2015112...20150401]
```
| 类型      | 使用实例 |
| :-------- |:--------|
| 月日年 | {date=mon_day_year:20150101-20150401}$ |
```
[01012015,112015,01122015,1122015...04012015]
```


```

* INT (整数)
支持如下三种类型
* 
```
{int=类型#长度$step:开始-结束}$
```

* STR (字符类型)

```
{str=类型#长度$step:开始-结束}$
```

* RE (正则引擎)

{re=引擎名称:正则表达式}$

``` python
{re=exrex:[0-9]}$
[0,1,2,3,4,5,6,7,8,9]
{re=exrex:(a|A)dmin[0-9]}$
[u'admin0',u'admin1',u'admin2',u'admin3',u'admin4',u'admin5',u'admin6',u'admin7',u'admin8',u'admin9',
 u'Admin0',u'Admin1',u'Admin2',u'Admin3',u'Admin4',u'Admin5',u'Admin6',u'Admin7',u'Admin8',u'Admin9']
```

## 安装
#### CentOS 6.* 7.* Linux
安装 setuptools, pip
``` shell
wget https://bootstrap.pypa.io/ez_setup.py -O - | python
wget https://pypi.python.org/packages/source/p/pip/pip-6.0.8.tar.gz
tar zvxf pip-6.0.8.tar.gz
cd pip-6.0.8
python setup.py install
```
安装 lxml解析器 & beautifulsoup4
``` shell
yum install python-devel libxml2-devel libxslt-devel
pip install lxml beautifulsoup4
```