1. 与django链接的话，首先创建一个django库app保存数据库引用scrapy（其实只要scrapy和django能互相链接即可），对这个库app注册，设置view（可以），并在其models.py下设置相应数据库文件并同步（同数据库中那个）
    
2. scrapy startproject scrapy_learn 设置settings
    
    ```python
        import os
        import sys
        import django
        sys.path.append(r'C:\Users\Crark\Desktop\hehe\python\djangotest')#django项目路径  
        os.environ['DJANGO_SETTINGS_MODULE'] = 'djangotest.settings'    # 项目名.settings
        django.setup()
    ```
    
    还有ROBOTSTXT_OBEY = False，User-Agent，ITEM_PIPELINES管道打开等
    
3. 创建spider ：scrapy genspider <spider名> < 域名>：spider头文件，在对应spider的py文件下下声明
    
    ```python
    import scrapy
    from xx.items import xxItem
    ```
    
4. item：scrapy中item.py 中引入django模型类 pip install scrapy-djangoitem后再item项目中引入(作者说：可理解为接受从爬取中传入的数据，实例化，并经行下一步传输，作用可以理解为激活，然后传给pipelines)
    
    ```python
    class xx(DjangoItem):
    # define the fields for your item here like:
    # name = scrapy.Field()           # 普通scrapy爬虫写法，用来定义字段（Fields）来描述要从网页中提取的数据
    # title = scrapy.Field()
    # url = scrapy.Field()
    # content = scrapy.Field()
    django_model = models.xx     # 注入django项目的固定写法，必须起名为django_model  =django中models.xx表
    ```
    
5. pipelines：痛苦面具,再settings里开启管道不要忘记
    
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
    
6. 关于scrapy主要就是spider文件到item文件再到pipelines文件，修改项目目录结构，让scrapy.cfg与manage.py同级，即删除项目目录中最外层的同名文件夹即整个下级目录向上移一级qaq
    
7. 还有一个scrapyd的安装，再scrapy目录下运行scrapyd可访问127.0.0.1 6800端口，scrapyd服务管理多个爬虫
    
8. 单独的scrapy运行时可以创建一个run.py用以下代码，连接mysql的话单独 pip install MySQLdb/pip install mysqlclient
    
    ```python
    from scrapy import cmdline
    ##注意，这里的lyw是作者在创建文件的时候最后一步的那个文件名，也就是spider中的py文件名
    cmdline.execute('scrapy crawl lyw'.split(' '))
    ```