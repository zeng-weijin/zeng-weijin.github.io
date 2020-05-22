### Centos7下的服务管理

#### 1.systemctl服务文件所在位置

```
/usr/lib/systemd/system/
```

#### 2.手动创建一个服务

手动编译安装的nginx是不会自动创建服务的，当我们希望它开机自启或者通过systemctl来控制时就可以手动创建一个nginx.service文件来实现。

```
# nginx.service
[Unit]
Description=nginx - high performance web server
After=network.target remote-fs.target nss-lookup.target

[Service]
Type=forking
ExecStart=/usr/bin/nginx -c /opt/nginx/conf/nginx.conf
ExecReload=/usr/bin/nginx -s reload
ExecStop=/usr/bin/nginx -s stop

[Install]
WantedBy=multi-user.target
```

> [Unit]:服务的说明
> Description:描述服务
>
> After:描述服务类别
>
> [Service]服务运行参数的设置
>
> Type=forking是后台运行的形式
>
> ExecStart为服务的具体运行命令
>
> ExecReload为重启命令
>
> ExecStop为停止命令
>
> PrivateTmp=True表示给服务分配独立的临时空间
>
> 注意：启动、重启、停止命令全部要求使用绝对路径
>
> [Install]服务安装的相关设置，可设置为多用户

#### 3.查看可用服务

```
systemctl list-unit-files
```

#### 4.查看运行中服务

```
systemctl list-units
```

#### 5.手动启动服务

```
systemctl start nginx.service
```

#### 6.停止服务

```
systemctl stop nginx.service
```

#### 7.设置开机自启动

```
systemctl enable nginx.service
```

#### 8.查看服务是否开机启动

```
systemctl is-enabled nginx.service
```

#### 9.查看服务状态

```
systemctl status nginx.service
```

#### 10.更多命令

```
使用systemctl --help进行了解
```

