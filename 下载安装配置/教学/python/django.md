# django建立项目
(django项目目录要好好看一下)  
pip install django
```django
	python环境路径
		- ...
		- scripts
			- pip.exe
			- django-admin.exe	【工具、创建django项目的文件和文件夹】
		- lib
			- 内置模块
			- site-package		【安装的第三方模块】
				- flask
				- ...
				- django		【框架的源码】
				- ...
		- python.exe
		- ...
```


1. 建立项目：django-admin.exe startproject xxxx 
2. 确定目录在xxxx下 创建app：python manage.py startapp  xx
3. 注册app 在settings.py 中installed_apps中注册xx（app xx
4. 接下来是简单跑一下 在url中添加（项目网页访问路径
    ```python
    from xx import views
        urlpatterns = [
            path('admin/', admin.site.urls),
            path('xx/', views.hello),
        ]
    ```  
5. 在xx的views下添加（views为xx对应后端吧
    ``` python
    from django.http import HttpResponse
        def hello(request):
            return HttpResponse("登录页面")
    ```
6. python manage.py runserver
7. 访问默认路径http://127.0.0.1:8000/xx/
# 关于网页和数据库的连接
1. settings里的设置:dirs为空，替换database里信息为自己mysql信息
2. 再xx文件夹下创建templates（网页）和static（css,js等静态文件）文件夹，创建网页记得再urls和view里声明和写函数
3. pip install pymysql 并在settings同级init下声明pymysql
    ``` python
    import pymysql
    pymysql.install_as_MySQLdb()
    ```
4. python manage.py inspectdb (单独表名) > models.py
5. 将models文件内容导入xx目录下的models，将文件中false改为true
6. 进行数据库关联：python manage.py makemigrations 和 python manage.py migrate，之后可以在views里添加后端相应
7. 表单连接后端的时候要加< form><% csrf_token %></ form>
8. 数据库关联之后要修改表设计的话，（我觉得这个最方便）要把models生成的init什么的先删掉，然后再数据库里删掉对应表，然后再django生成表django_migrations里删除生成记录，然后重新生成。
# [[scrapy]]
1. 与django链接的话，首先创建一个django库app保存数据库引用scrapy（其实只要scrapy和django能互相链接即可），对这个库app注册，设置view（可以），并在其models.py下设置相应数据库文件并同步（同数据库中那个）
1. scrapy startproject scrapy_learn 设置settings
    ```python
        import os
        import sys
        import django
        sys.path.append(r'C:\Users\Crark\Desktop\hehe\python\djangotest')#django项目路径  
        os.environ['DJANGO_SETTINGS_MODULE'] = 'djangotest.settings'    # 项目名.settings
        django.setup()
    ```
    还有ROBOTSTXT_OBEY = False，User-Agent，ITEM_PIPELINES管道打开等
2. 创建spider ：scrapy genspider <spider名> < 域名>：spider头文件，在对应spider的py文件下下声明
    ```python
    import scrapy
    from xx.items import xxItem
    ```
3. item：scrapy中item.py 中引入django模型类  pip install scrapy-djangoitem后再item项目中引入(作者说：可理解为接受从爬取中传入的数据，实例化，并经行下一步传输，作用可以理解为激活，然后传给pipelines)
    ```python
    class xx(DjangoItem):
    # define the fields for your item here like:
    # name = scrapy.Field()           # 普通scrapy爬虫写法，用来定义字段（Fields）来描述要从网页中提取的数据
    # title = scrapy.Field()
    # url = scrapy.Field()
    # content = scrapy.Field()
    django_model = models.xx     # 注入django项目的固定写法，必须起名为django_model  =django中models.xx表
    ```
4. pipelines：痛苦面具,再settings里开启管道不要忘记
    ```python
    from asgiref.sync import sync_to_async
    class Scrapy1Pipeline(object):
        @sync_to_async
        def process_item(self, item, spider):
            print('打开了数据库')
            item.save()
            print('关闭了数据库')
            return item
    ```
4. 关于scrapy主要就是spider文件到item文件再到pipelines文件，修改项目目录结构，让scrapy.cfg与manage.py同级，即删除项目目录中最外层的同名文件夹即整个下级目录向上移一级qaq

5. 还有一个scrapyd的安装，再scrapy目录下运行scrapyd可访问127.0.0.1 6800端口，scrapyd服务管理多个爬虫

6. 单独的scrapy运行时可以创建一个run.py用以下代码，连接mysql的话单独 pip install MySQLdb/pip install mysqlclient
    ```python
    from scrapy import cmdline
    ##注意，这里的lyw是作者在创建文件的时候最后一步的那个文件名，也就是spider中的py文件名
    cmdline.execute('scrapy crawl lyw'.split(' '))
    ```








