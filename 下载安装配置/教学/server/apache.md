1. 在httpd.conf里修改目标路径 端口等等，以下是conf里要更改的一些
2. 目录都反杠反杠
	+ `Define SRVROOT "D:/learn/server/Apache24"`（服务器路径
	+ `ServerName www.localhost.com:80` （访问网页路径
	+ ```
			<Directory />
			    AllowOverride none
			    Require all granted
			</Directory> ```    
	+  ```
			<IfModule dir_module>// 目标网页，要在本机上设置多个网页的需要另外的技能
			    DirectoryIndex index.html
			</IfModule>```
	+ ```
				#将PHP配置文件加载到Apache配置文件中，共同生效
				PHPIniDir D:/learn/server/php8
				#加载PHP
				LoadModule php_module D:/learn/server/php8/php8apache2_4.dll
				#配置Apache分配工作给PHP模块，把PHP代码交给PHP处理
				#即.php后缀名的文件
				AddType application/x-httpd-php .php```
3.  ```
			php.ini中打开扩展（php还有其他配置在这里就不赘述了qaq
			extension_dir = "D:/learn/server/php8/ext"
			extension=mysqli
			extension=pdo_mysql```
4. cmd 
	+ httpd -t验证   
	+ httpd -k install -n "apache"安装   
	+ httpd -k uninstall -n Apache
	+ httpd -k install -n Apache2.4

注意：如果在cmd中输入命令不好使那么直接进入注册表删除即可，切记操作完一定要重启电脑，然后在操作其他的如果执行代码成功后进入注册表里没发现有Apache服务，那么也证明卸载干净了，重启电脑即可1、关闭服务器，以管理员运行cmd进入Apache24/pin目录下运行 httpd -k uninstall -n apache2.4 
2、打开注册表管理器，Win+R => regedit HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services