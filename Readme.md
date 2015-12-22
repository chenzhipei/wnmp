## Windows下配置nginx+php环境

### 下载
安装 PHP <http://windows.php.net/download/>

下载"no-install"zip包，并解压到"php"文件夹内。

安装 Nginx <http://nginx.org/>

下载 Nginx 并解压到 "nginx" 文件夹内。

需要 RunHiddenConsole.zip

下载 [RunHiddenConsole.zip](http://redmine.lighttpd.net/attachments/660/RunHiddenConsole.zip)，解压到nginx与php目录内。

### 配置服务
#### php
进入"php"文件夹，复制"php.ini-recommended",重命名为"php.ini"，并用Editplus或者Notepad++打开来，找到：
```bash
;extension_dir = "ext"
```

去掉之前的";" 并更改为：
```bash
extension_dir = "G:\php\ext"    #这里是php下ext的路径
```

配置php，让php能够与nginx结合，找到：
```bash
;cgi.fix_pathinfo=1
```

去掉之前的";"
```bash
cgi.fix_pathinfo=1
```

####nginx
进入nginx的conf目录，打开nginx的配置文件nginx.conf，找到
```bash
location / {
      root   html;　　　　　　#这里是站点的根目录，更改为你项目的路径
      index  index.html index.htm;
}
```

再往下，找到
```bash
# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
#
#location ~ \.php$ {
#    root           html;
#    fastcgi_pass   127.0.0.1:9000;
#    fastcgi_index  index.php;
#    fastcgi_param  SCRIPT_FILENAME  /scripts$fastcgi_script_name;
#    include        fastcgi_params;
#}
```

先将前面的“#”去掉，同样将"html"改为站点的路径，再把"/scripts"改为"$document_root"，这里的"$document_root"就是指前面"root"所指的站点路径，这是改完后的：
```bash
# pass the PHP scripts to FastCGI server listening on 127.0.0.1:9000
#
location ~ \.php$ {
      root           G:/rainloop;
      fastcgi_pass   127.0.0.1:9000;
      fastcgi_index  index.php;
      fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
      include        fastcgi_params;
}
```
保存配置文件

### 启动服务
确定每个文件都放在指定的文件夹后，运行"start_server.bat"启动服务，双击"stop_server.bat"停止服务。


###备注：
--------------------------------------------------------------------------------
1、"start_server.bat"和"stop_server.bat"可参考我给出的例子。

2、具体详细配置:http://www.cnblogs.com/huayangmeng/archive/2011/06/15/2081337.html
