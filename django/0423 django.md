# Django的使用

## Django简介：

Django是一个开放源代码的Web应用框架，由Python写成。采用了MTV的框架模式，即模型M，模板T和视图V。它最初是被开发来用于管理劳伦斯出版集团旗下的一些以新闻内容为主的网站的，即是CMS（内容管理系统）软件。并于2005年7月在BSD许可证下发布。这套框架是以比利时的吉普赛爵士吉他手Django Reinhardt来命名的。

## MTV模式简介

MTV模式在本质上与MVC模式没有区别，都是为了解耦各个组件，只是在定义上有些不同。

Model: 负责业务与数据库的对象

View: 负责业务逻辑并适当调用Model和Template

Template： 负责把页面渲染展示给用户

注意： Django中还有一个url分发器，也叫做路由。主要用于将url请求发给不同的View处理，View再进行处理

## 安装VIRTUALENV（windows)

1. 安装virtualenv

    
```
pip install virtualenv
```

2. 创建虚拟环境

在本地创建一个叫env的文件夹，并且Cd到该文件夹下输入：

```
virtualenv --no-site-package testenv
```

3. 进入虚拟环境


```
cd env/testenv/Scripts>activate

退出: deactivate
```

## 创建Django项目

### 在虚拟环境中安装django和pymysql


```
pip install pymysql

pip install django==1.11
```

### 创建一个Django项目
首先要在虚拟环境中cd到你创建的项目文件夹：
![这里写图片描述](https://img-blog.csdn.net/20180423195324563?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzQxNzY4NDIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

然后输入：
```
django-admin startproject helloworld
```

创建好之后，目录下有这些文件：

![这里写图片描述](https://img-blog.csdn.net/20180423195948718?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzQxNzY4NDIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

manage.py： 是Django用于管理本项目的管理集工具，之后站点运行，数据库自动生成，数据表的修改等都是通过该文件完成。

init.py： 指明该目录结构是一个python包，暂无内容，在后期会初始化一些工具会使用到。

seetings.py： Django项目的配置文件，其中定义了本项目的引用组件，项目名，数据库，静态资源，调试模式，域名限制等

urls.py：项目的URL路由映射，实现客户端请求url由哪个模块进行响应。

wsgi.py：定义WSGI接口信息，通常本文件生成后无需改动

### 创建应用

1. cd到helloword文件下，创建一个叫stu的app,输入：


```
python manage.py startapp stu
```

2. 进入helloword文件的settings里，找到如下代码并在最后加入'stu'，此过程为激活应用:

![这里写图片描述](https://img-blog.csdn.net/20180423201000321?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzQxNzY4NDIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

### app实例
1. 配置数据库

    注意：django默认使用SQLite数据库
    
    在settings.py文件中，通过DATABASES选项进行数据库配置
    
    配置MySQL
        
        1. python3,安装的是PyMySQL
        
        2. 在_init_.py文件中写入两行代码：
        
            import pymysql
        
            pymysql.install_as_MySQLdb()
        
        3. 将ENGINE后的sqlite换成mysql，将NAME中的内容换成我们自己的数据库名称
        
        4. 添加：
        
            ‘USER':'root',
            'PASSWORD':'123456'
            'HOST':'localhost'
            'PORT':'3306'
    具体效果如图：

![这里写图片描述](https://img-blog.csdn.net/20180423202044294?watermark/2/text/aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3NpbmF0XzQxNzY4NDIz/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70)

2. 找到stu下的views文件，在里面创建一个添加学生的类：


```
from django.shortcuts import render
from django.http import HttpResponse

def addStudent(request):

    return HttpResponse('添加成功')
```

3. 在stu的文件下新建一个叫urls.py的python文件，在其中输入：


```
from django.conf.urls import url
from stu import views

urlpatterns = [
    url(r'addstu/',views.addStudent)
]
```
4. 定义模型

    进入stu中的models.py文件中，输入以下代码创建一个学生模型（也对应一个数据表）：
    
    
```
from django.shortcuts import render

# Create your models here.

class Student(models.Model):
    name = models.CharField(max_length=20)
    sex = models.BooleanField()

    class Meta:
        db_table = 'stu'
```


4. 在数据库中添加数据表

cd到helloword下，输入以下代码生成迁移文件：

```
python manage.py  makemigrations
```

执行迁移文件：


```
python manage.py migrate
```

5. 向数据表中添加数据：

进入到stu下的views中，输入以下代码：


```
from django.shortcuts import render
from django.http import HttpResponse
# Create your views here.

from models import Student

def addStudent(request):

    stu = Student()
    stu.name = '张三'
    stu.sex = 1
    stu.save()
    
    return HttpResponse('添加成功')
```


