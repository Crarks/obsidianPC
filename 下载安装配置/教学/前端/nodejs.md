#### 新建node（每个项目都要初始化
+ 输入初始化命令：npm init -y[^1][^2]
+  安装express 模块：npm i express
+ 安装mysql模块：npm i mysql
+ 每个项目都要初始化
	
[^1]: 创建出的两个package文件相当于下载插件的声明那种。 
[^2]: 命令npm -v 、npm install等都无法使用，直接卡住不动。解决办法：在C: \\ Users \\ Administrator里面有一个.npmrc的隐藏文件，将其直接删掉就能解决npm命令卡死的情况 
#### node服务器
+ 直接一个小代码示例一下，要打开index界面的话需要单独创建一个
```node
//请求express
var express = require('express');
//创建express对象
var app = express();
//请求mysql
var mysql  = require('mysql');
//设置数据库连接信息
const bodyParser = require('body-parser');  
/*bodyParser模块是一个HTTP请求体解析中间件
可以轻松地获取前端传过来的post信息。加载body-parser后，
通过req.body即可获取前端传过来的post信息
*/
//用户登录------------------------------
var connection = mysql.createConnection({    
host     : 'localhost',      
user     : 'root',            
password : '888888',      
port: '3306',                  
database: 'nodejs'
});
//建立连接
connection.connect();
//设置静态文件路径,默认打开的使打开的就是public中的index
//就是不添加app.get也可以打开public中的index
app.use(express.static('public'));
//在浏览器中访问localhost:3000,默认打开index.html页面
app.get('/', function (req, res) {
    res.sendFile( __dirname + "/" + "index.html" );
})
//创建实现登录功能的路由，处理GET请求  
app.get('/login',function (req,res) {  
    //获取用户输入的账号，密码  
    var response = {  
    "username":req.query.username,  
    "password":req.query.password,  
    };  
   //创建查询数据的sql语句实现登录功能，查询账号和密码并且与用户输入的账号密码完全一致  
    var selectSQL = "select username,password from nodejs where username = '"+req.query.username+"' and password = '"+req.query.password+"'";  
    //进行数据库操作  
    connection.query(selectSQL,function (err, result) {  
        //打印错误信息  
        if(err){  
        console.log('[login ERROR] - ',err.message);  
        return;  
        }  
        //如果查询结果为空，则登录失败，否则登录成功  
        if(result=='')  
        {  
            console.log("帐号密码错误");  
            res.end("fail");  
        }  
        else  
        {  
            console.log("sussess");  
            res.end("success");  
        }  
    });  
    console.log(response);  
})  
//过滤所有嵌套
app.use((req, res, next) => {  
    res.setHeader('Content-Security-Policy', 'default-src \'self\'; frame-ancestors \'none\'');  
    next();  
  });
//取消script过滤
//允许内联脚本和通过 eval 执行的脚本
app.use((req, res, next) => {  
    res.setHeader('Content-Security-Policy', "default-src 'self'; frame-ancestors 'none'; script-src 'self' 'unsafe-inline' 'unsafe-eval' example.com");  
    next();  
});
//输入返回------------------------------
//创建实现提交功能的路由，处理POST请求  
app.use(bodyParser.urlencoded({ extended: false }));  
app.use(bodyParser.json()); 
app.post('/submit', function (req, res) {    
    const userInput = req.body.userInput;    
    res.send(`您输入的内容是：${userInput}`);    
});
//创建服务器
var server = app.listen(3000, function () {
    console.log("访问地址为 localhost:3000")
})
```