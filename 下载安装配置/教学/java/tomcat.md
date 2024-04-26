+ 默认端口8080 启动cmd startup.bat，访问127.0.0.1即可
+ conf下服务器配置
	+ server.xml是Tomcat的主配置文件（全局）,服务器设置的，例如端口设置，路径设置。
	+ context里设置tomcat数据源，用来连接数据库。
	+ tomcat_user主要是用户名和密码的设置。
	+ web是默认首页等等之类的设置
	+ conf->logging.properties 大概在51行utf修改为gbk解决启动乱码问题  

突然想起来，tomcat原先没配出来，实际上是idea直连的，唔，那就不把我半成品的学习放上来了qaq
