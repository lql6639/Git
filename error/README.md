## `Git Error`

### `1、GitHub官网打不开的解决办法`

+ **1、获取github官网ip**

> **`WIN+R`打开`cmd`，然后`ping github.com`，假如发现`github.com`的地址是`20.205.243.166`**

+ **2、配置hosts文件，绕过DNS解析**

> **打开电脑`C:\Windows\System32\drivers\etc`下的`hosts`文件编辑（需要管理员权限，右键，管理员权限打开），新增如下一行配置**

```shell
20.205.243.166 github.com
```

+ **3、刷新DNS缓存**

> **`WIN+R`打开`cmd`，输入如下指令刷新DNS缓存**

```shell
ipconfig /flushdns
```

### `2、GitHub官网打不开或访问慢备选方案1`

> **如果还是不能解决，就到<https://ipaddress.com>分别查询`github.com`和`github.global.ssl.fastly.net`的`ip`值**
>
> **假如查询出来ip分别为`140.82.113.4`和`199.232.69.194`配置到了hosts文件中的：**

```shell
140.82.113.4 github.com

199.232.69.194 github.global.ssl.fastly.net
```

> **然后再次刷新dns缓存，再试试访问github，应该就可以了**

### `3、GitHub官网打不开或访问慢备选方案2`

> **在`gitee`上有个开源项目名为 `dev-sidecar`，为开发者打辅助的边车工具，通过本地代理的方式将https请求代理到一些国内的加速通道上**
>
> **通过修改sni实现 github 直连加速 ，还支持一些 clone加速、头像加速、npm加速等等功能，具体的操作直接到项目的readme参考即可**

> **以上就是github官网打不开或访问慢的解决办法，相信你已经学会了，可以快乐地在github里玩耍了**

### `4、打开GitHub官网后页面乱码的解决办法`

+ **1、获取请求网址**

> **按`F12`，在开发者工具查看`网络`面板的`请求网址`，假如发现github的请求网址为`https://github.githubassets.com/...`**

+ **2、查询电脑可达ip**

> **打开dns查询工具网站<https://tool.chinaz.com/dns>，根据github的请求网址进行`查询电脑可达ip`，`选择ttl值最大的`，`ping一下`**

+ **3、配置hosts文件，绕过DNS解析**

> **假如发现ttl值最大的ip地址是`185.199.108.154`，然后配置`hosts`文件，绕过DNS解析**
>
> **打开电脑`C:\Windows\System32\drivers\etc`下的`hosts`文件编辑（需要管理员权限，右键，管理员权限打开），新增如下一行配置**

```shell
185.199.108.154 github.githubassets.com
```

+ **4、刷新DNS缓存**

> **`WIN+R`打开`cmd`，输入如下指令刷新DNS缓存**

```shell
ipconfig /flushdns
```

+ **5、重启电脑**

> **刷新DNS缓存，断网重连后发现并没有生效，重启电脑**
