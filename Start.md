# 开始食用
# 伪静态
## apache
```
Options -MultiViews

RewriteEngine On

RewriteCond %{REQUEST_FILENAME} !-f

RewriteRule ^ index.php [QSA,L]
```
## nginx
```
rewrite ^ /index.php last;
```
## caddy2
```
@key0 {
 not file 
 path_regexp key0 ^ 
}
rewrite @key0 /index.php
```
# 定义路由
> 将此框架项目打开后，可以看到根目录有app.php  
> 已经有一个示例在里边，他写的是：  
```php
App::use('',__routes__.'/index/index.php'); 
```
>  
> 观察他  
> 第一部分，命令部分：App::use();  
> 第二部分：第一个参数：路由的名称，如果你填写'/'或''，那么就是 http://host/ 或 http://host 就可以执行第二个参数，否则不执行，跳出404  
> 第二个参数，路由文件目录，请在根目录下的routes创建路由文件，然后使用[__routes__]变量：
```php
__routes__.'你路由文件名称.php';
```
# 路由文件规则
> 框架内已有示例：index.php的路由文件  
> 不可定义：stylesheets;javascripts;images;fonts;data,这几个路由为静态文件路由,通过系统变量引入，请查看全局变量

> 路由文件模板为：
```php
class Index{
    public function start(YM_request $request){
		
    }
}
```
> 路由文件名称随意，看你喜好  
- 类名必须为Index
- 类名必须有public的方法，且方法名称为：start
- 类名必须接收参数：YM_request类型，为了规范，变量名称请取$request  

> 至此你已经会了80%
# YM_request类
## 获取post参数  
> post('key') 
## 获取get参数  
> get('key') 
## 获取post与get参数  
> request('key') 
## 获取params参数
> /dd/ww这种,可获取dd ww 或/dd/index.html 可获取dd index.html  
> query()
## 当前请求是否是get
> whetherGet() 
## 当前请求类型
> requestType()  
## 输出报错信息
>直接输出报错信息  
> error($ocde,$msg)  
> $code:返回状态码  
> $msg:返回报错内容  
## 获取body参数
> 全部  
> body() 
## 获取请求头  
> header() 
## 输出内容
> send($msg)  
> $msg:输出内容
## 输出文件内容
> sendFile($path)  
> $path:文件绝对路径  
## 输出模板内容
> render($path,$options)  
> $path:文件绝对路径  
> $options:模板变量,array类型，比如：['title'=>'这是标题'] 
## 请求头取cookies
> header_cookies() 从请求头取cookies  
## 取cookies  
> cookies() 取cookies  
## 获取请求ip
> ip() 获取请求ip  
## 字符串净化
> purge($string,$trim = true,$filter = true,$force = 0, $strip = FALSE)  
> $string:需要净化的字符串  
## 获取日志  
> getLog  
## 获取ip  
> ipV2(int $type = 0,string $ipServer=NULL)  
> $type:默认0HTTP_CLIENT_IP，1HTTP_X_FORWARDED_FOR，2REMOTE_ADDR，3REMOTE_ADDR，4自定义，需要在参数二给出  
> $ipServer:自定义获取ip头比如：HTTP_CLIENT_IP
## 返回自定义状态页面。比如404页面等等
> statusPage(int $response_code,string $path,array $options=[])  
> $response_code:状态码
> $path:页面路径
> $options:页面参数传递，老样子{{表示变量}}

# YM_Class类
> 先 new YM_Class()
## 发送邮件 
> $YM_Class->send_mail($host, $port, $user, $pass, $to, $content = NULL, $title = 'YM框架邮件系统', $type = 'TXT', $debug = false)  
> 参数详解：    
> $host:邮件服务器  
> $port:邮件端口  
> $user:邮件账号  
> $pass:邮件密码  
> $to:发送给谁  
> $content:发送的内容，可以html  
> $title:邮件标题  
> $type:发送类型  
> $debug:debug  
## 取文本中间
> $YM_Class->txt_zhong($str, $leftStr, $rightStr) 
> 参数详解：  
> $str:需要取中间的文本
> $leftStr:左边文本
> $rightStr:右边文本
## 取文本右边
> $YM_Class->txt_zhong($str, $leftStr) 
> 参数详解：  
> $str:需要取右边的文本
> $leftStr:左边文本
## 取文本左边
> $YM_Class->txt_zhong($str, $rightStr) 
> 参数详解：  
> $str:需要取左边的文本
> $rightStr:右边文本
## RC4加解密
> $YM_Class->mi_rc4($data, $pwd, $t = 0)
> 参数详解：  
> $data:需要加解密的文本
> $pwd:密码
> $t:模式。0加密，1解密
## RSA公钥加解密(分段,超过密钥长度分段加解密)
> $YM_Class->RSA_GMI($data, $key, $t = 0)
> 参数详解：  
> $data:需要加解密的文本
> $key:公钥
> $t:模式。0加密，1解密
## RSA私钥加解密(分段,超过密钥长度分段加解密)
> $YM_Class->RSA_SMI($data, $key, $t = 0)
> 参数详解：  
> $data:需要加解密的文本
> $key:私钥
> $t:模式。0加密，1解密
## 随机字符串
> $YM_Class->getRandom($number)
> 参数详解：  
> $number:长度
## 获取毫秒时间戳
> $YM_Class->getMillisecond()
# 数据库类
> 未实例化，实例化需要数据库账号，密码，地址，数据库名，端口号  
## 实例化数据库类
> 需要连接sqlite,自定义常量为：SQLITE，并设定为true，布尔,同时sqlite数据库后缀名保持为空(不要后缀名db 安全)  
> new DB("db数据库路径")  
> mysql数据库，自动判断新旧类型
> new DB($db_host, $db_user, $db_pass, $db_name, $db_port)  
> 参数详解：  
> $db_host:数据库地址  
> $db_user:数据库账号  
> $db_pass:数据库密码  
> $db_name:数据库名  
> $db_port:数据库端口号
##数据库类方法
## query($sql)  
> 执行sql语句  
## fetch($sqlquery)  
> 取结果集(1个)  
> 参数详解：  
> $sqlquery:query($sql)执行后返回的类  
## fetch_all($sqlquery)
> 取结果集(所有 7.0以上)  
> 参数详解：  
> $sqlquery:query($sql)执行后返回的类  
## get_row_all($sql)
> 取结果集(所有 7.0以上)  
> 参数详解：  
> $sql:sql语句  
## multi_query($sql)
> 执行多行sql语句，布尔返回  
> 参数详解：  
> $sql:sql语句  
## count($sql)  
> 取结果集数量  
## get_row($sql)  
> 取结果集（1个）  
## mysqli_fetch_assoc($sqlquery)
> 取结果集（1个），需要循环，循环就是所有结果集,推荐使用get_row_all或fetch_all
```php
while($row= mysqli_fetch_assoc($sqlquery)){
    //每一次循环就是一个结果集(一条)
}
```	
> 参数详解：  
> $sqlquery:query($sql)执行后返回的类
## insert($sql)  
> 执行插入语句  
> 参数详解：  
> $sql:只允许放入insert语句，取插入id  
## error()  
> 取错误信息  
## escape()  
> 转义特殊字符  
## affected()   
> 使用query()后，再执行此方法，获取受影响的行数。一个 > 0 的整数表示所影响的记录行数。0 表示没有受影响的记录。-1 表示查询返回错误。  
## insert_array($table,$array)
> 执行插入语句,表字段较多可以用这个简洁  
> 参数详解：  
> $table:表名  
> $array:插入键值对，格式：['键'=>'','键1'=>'值2'...]。键名必须与字段名一样