# 开始食用
# 定义路由
> 将此框架项目打开后，可以看到根目录有app.php  
> 已经有一个示例在里边，他写的是：  
> App::use('',__routes__.'/index/index.php');  
> 观察他  
> 第一部分，命令部分：App::use();  
> 第二部分：第一个参数：路由的名称，如果你填写'/'或''，那么就是 http://host/ 或 http://host 就可以执行第二个参数，否则不执行，跳出404  
> 第二个参数，路由文件目录，请在根目录下的routes创建路由文件，然后使用__routes__变量：__routes__.'你路由文件名称.php';
# 路由文件规则
> 框架内已有示例：index.php的路由文件  

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
> body_post('key') 
## 获取get参数  
> query_get('key') 
## 获取post与get参数  
> request('key') 
## 当前请求是否是get  
> is_get() 
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
# YM_Class类
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
## RSA公钥加解密
> $YM_Class->RSA_GMI($data, $key, $t = 0)
> 参数详解：  
> $data:需要加解密的文本
> $key:公钥
> $t:模式。0加密，1解密
## RSA私钥加解密
> $YM_Class->RSA_SMI($data, $key, $t = 0)
> 参数详解：  
> $data:需要加解密的文本
> $key:私钥
> $t:模式。0加密，1解密