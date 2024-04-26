https://blog.csdn.net/zhimi520/article/details/128826192
sudo passwd root  
su root  
sudo apt-get update更新安装源  
sudo apt-get install net-tools ifconfig   
sudo apt-get install openssh-server ssh  
sudo service ssh start  启动ssh  
sudo ps -e | grep ssh 有sshd启动成功  
sudo systemctl disable --now ssh 禁用ssh  
sudo systemctl enable --now ssh 启用ssh  
vim /etc/ssh/sshd_config  找到 PermitRootLogin 去掉前边的 # ，修改为 PermitRootLogin yes (vi和vim是两种东西qnmd) 
sudo service ssh restart  保存后重启 ssh 服务 

crtl + d返回上一级用户  
exit 退出永户

vim /字符查询，n查询下一处，N（大写N）就会向前查询



https://www.cnblogs.com/Horizon-asd/p/14888903.html ryu远程连接啥的
https://blog.csdn.net/iroy33/article/details/102488949 min基本命令啥的
[安装 | Mininet 应用与源码剖析 (gitbook.io)](https://yeasy.gitbook.io/mininet_book/introduction/install)

https://blog.csdn.net/kling_bling/article/details/127272819

[Exception: Could not find a default OpenFlow controller - tycoon3 - 博客园 (cnblogs.com)](https://www.cnblogs.com/dream397/p/13335666.html) 不明觉厉