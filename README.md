# chfs-file-server
使用CuteHttpFileServer 搭建静态文件服务器 分享文件 图床



##### 下载地址：http://iscute.cn/chfs


## Linux

下载 [chfs-linux-amd64-2.0.zip](http://iscute.cn/tar/chfs/2.0/chfs-linux-amd64-2.0.zip) 

```
wget http://iscute.cn/tar/chfs/2.0/chfs-linux-amd64-2.0.zip
```

解压

```
unzip chfs-linux-amd64-2.0.zip
```

给执行权限

```
chmod +x chfs
```

一点建议

```
//需要放在path目录（bin/sbin），否则需修改path。
//如放在目录/usr/local/bin目录 
chmod +x /usr/local/bin/chfs
```

简单启动测试

```
//共享目录，监听端口号为8080
chfs --path="./" --port=8080
```

保持后台运行

```
//安装screen
apt install screen

//共享目录为根目录下的/web，监听端口号为8080
screen  chfs --path="./web/" --port=8080

//后台运行根目录下的配置文件chfs.ini
 screen chfs --file="./chfs.ini"
```

退出screen

```
//退出screen，先查找screen的进程序号
pgrep screen
//杀死进程
kill ******（上步得到的序号）
```


### 配置



```
#---------------------------------------
# 请注意：
#     1，如果不存在键或对应值为空，则不影响对应的配置
#     2，配置项的值，语法如同其对应的命令行参数
#---------------------------------------

# 监听端口
port=666

# 共享根目录，通过字符'|'进行分割
# 注意：
#     1，带空格的目录须用引号包住，如 path="c:a uply namefolder"
#     2，可配置多个path，分别对应不同的目录
path="/"


# IP地址过滤
allow=


#----------------- 账户控制规则 -------------------
# 注意：该键值可以同时存在多个，你可以将每个用户的访问规则写成一个rule，这样比较清晰，如：
#     rule=::R
#     rule=root:123456:RW
#     rule=readonlyuser:123456:R
#    匿名用户具有只读权限（默认情况下匿名用户具有读写权限） 账户admin，密码为admin123，具有读写删权限
#  rule=::r|admin:admin123:rw
rule=::R|admin:admin123:RWD

# 用户操作日志存放目录，默认为空
# 如果赋值为空，表示禁用日志
log=
# 网页标题
html.title=文件服务

# 网页顶部的公告板。可以是文字，也可以是HTML标签，此时，需要适用一对``(反单引号，通过键盘左上角的ESC键下面的那个键输出)来包住所有HTML标签。几个例子：
#     1,html.notice=内部资料，请勿传播
#     2,html.notice=`<img src="https://mat1.gtimg.com/pingjs/ext2020/qqindex2018/dist/img/qq_logo_2x.png" width="100%"/>`
#     3,html.notice=`<div style="background:black;color:white"><p>目录说明：</p><ul>一期工程：一期工程资料目录</ul><ul>二期工程：二期工程资料目录</ul></div>`
html.notice=内部资料，请勿传播

# 是否启用图片预览(网页中显示图片文件的缩略图)，true表示开启，false为关闭。默认开启
image.preview=true

# 下载目录策略。disable:禁用; leaf:仅限叶子目录的下载; enable或其他值:不进行限制。
# 默认值为 enable
folder.download=

#-------------- 设置生效后启用HTTPS，注意监听端口设置为443-------------
# 指定certificate文件
ssl.cert=
# 指定private key文件
ssl.key=
# 设置会话的生命周期，单位：分钟，默认为30分钟
session.timeout=

```

