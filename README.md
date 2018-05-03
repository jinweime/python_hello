
* 1. 新建django项目


![](https://ws4.sinaimg.cn/large/006tKfTcly1fqyh809lwoj316y0qgdh4.jpg)
* 2.*创建一个名字叫app的程序 django中不管是博客还是一个站点都是一个application，所以我们需要命名我们自己的applicaiton。*

```
python3 manage.py startapp app
```

生成后的目录结构
![](https://ws4.sinaimg.cn/large/006tKfTcly1fqyh9dhfarj30ws0ge3yt.jpg)

执行完后出现了一个app的目录
![](https://ws4.sinaimg.cn/large/006tKfTcly1fqyer5ehh3j30b60doaa6.jpg)

* 3.配置环境
在vpnpage目录下面找到setting.py 文件的INSTALLED_APPS数组，把我们刚刚新建的app加入到apps中

```
INSTALLED_APPS = [
    'django.contrib.admin',
    'django.contrib.auth',
    'django.contrib.contenttypes',
    'django.contrib.sessions',
    'django.contrib.messages',
    'django.contrib.staticfiles',
    'app'
]
```


*templates中创建一个html文件
app中找到views.py进入一个view路径*

```
from django.shortcuts import render


# Create your views here.
def index(request):
    return render(request, 'index.html')
```


vpnpage目录下找到urls.py进入一个urlpath路径


```
from django.contrib import admin
from django.urls import path
from django.conf.urls import url
from app.views import index

urlpatterns = [
    path('admin/', admin.site.urls),
    url(r'^index/', index),//^是正则表达优化index?id=2的找不到网页情况
]
```

* 4.用static目录来加载css文件

通过{% load %}标签来加载我们的css
![](https://ws3.sinaimg.cn/large/006tKfTcly1fqyhk1s3mmj30kg0ieglu.jpg)

```
{% load static %}
<html>
<head>
    <link rel="stylesheet" type="text/css" href="{% static 'mycss.css' %}">
    <meta charset="UTF-8">
    <title>Untitled Document</title>
</head>
<body>

<h1>h1</h1>
<h2>h2</h2>
<h3>h3</h3>
<h4>h4</h4>
<h5 style="background:#A65E60 ">h5</h5>
<h6>h6</h6>

<p>this is p标签</p>
<p>this is p标签</p>

<a href="http://www.baidu.com">google</a>


<img src="{% static 'aaaa.jpg' %}" width="40" height="50">
</body>
</html>




```

setting.py加入一个static静态文件的变量
```
STATICFILES_DIRS = (os.path.join(BASE_DIR, "static"),)
```

*运行当前的web项目*
```
python3 manage.py runserver
```

![](https://ws3.sinaimg.cn/large/006tKfTcly1fqyhnrzbh4j31kw0cf3z5.jpg)


**注意 域名后面记得加入我们定义的urls路径 index**
http://127.0.0.1:8000/index/通过这个地址就能正常访问了
