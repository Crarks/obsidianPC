感觉知识点很杂的样子   

### 实验一
###### 基本概念
+ ac(huawei)/wlc(cisco)接入控制器（路由器、交换机给予管理ap的功能
+ ap 无线接入点access point（相当用于接入的二层交换机 ，市面上有胖瘦功能区分的机子
+ poe交换机
+ esight 支持多设备管理巴拉巴拉
+ radius RADIUS（Remote Authentication Dial-In User Server，远程认证拨号用户服务）是一种分布式的、C/S架构的信息交互协议，能包含网络不受未授权访问的干扰，常应用在既要求较高安全性、又允许远程用户访问的各种网络环境中。
###### ac初始化配置
[参考](https://blog.csdn.net/weixin_44505445/article/details/126150308)  
[参考](https://www.bilibili.com/video/BV11g411p72h/?spm_id_from=333.788&vd_source=b0f7689f6d719082f5b29fa96034f7a4)  

*交换机*
1. 创建vlan10 11 12 13，将连结ac和ap的接口设置为trunk并缺省为vlan10
2. 添加loopback ip和vlan虚拟接口的网关  

*AC*
[参考](https://blog.csdn.net/2302_78039953/article/details/135960548)  
1. 添加wcl ip和ap插电源，添加vlan5允许pc和wcl通信
2. pc登录 第一次用http 之后用https登录
3. 再controllers interface添加vlan接口
4. 添加vlan，注意几个enable（没配radius的WPA2-Enterprise安全策略


登不上网页的话好像是因为wlc-pt这个型号的问题,不能访问啥的
[参考](https://learningnetwork.cisco.com/s/question/0D53i00001OEtFcCAL/how-to-fix-the-server-reset-connection-error-in-wlc)
呵呵 b溃了，不做了呵呵
总之再要做的话不管vlan，直接先做radius和aaa脸上sta，就跟上面有一个参考做