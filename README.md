# docker-lnmp

docker-compose一键部署lnmp+redis环境，集成php7.1+php7.3+php7.4+php8.1+php8.2+php8.3

##  文件结构

```
│
│  docker-compose.yml
│  
├─conf	//配置文件
│  ├─mysql8.0
│  │      my.cnf
│  │      
│  ├─nginx
│  │  │  nginx.conf
│  │  │  
│  │  └─conf.d	//nginx转发配置
│  │          default.conf
│  │          
│  └─redis
│          redis.conf
│          
├─data	//数据库文件
│  ├─mysql8.0
│  │          
│  └─redis
│              
├─logs	//日志
│  ├─mysql8.0
│  │     
│  └─nginx
│          
├─php		//多版本php
│  ├─php7.1-fpm
│  │      dockerfile
│  │      
│  ├─php7.3-fpm
│  │      dockerfile
│  │      
│  ├─php7.4-fpm
│  │      dockerfile
│  │      
│  ├─php8.1-fpm
│  │      dockerfile
│  │      
│  ├─php8.2-fpm
│  │      dockerfile
│  │      
│  └─php8.3-fpm
│         dockerfile
│          
└─workspace	//项目根目录
```

## 使用方法

启动：

```bash
docker-compose up -d
```

## 注意事项

1.   开发大型项目/框架时（Eg: Laravel），如遇到http请求本地接口（排除网络因素）响应慢的情况，请先将docker设置取消勾选wsl2后再进行构建docker-compose。
2.   各php版本、nginx、mysql、redis是基于官方镜像源（debian）打包发布的。
3.   如遇到缺少php扩展的情况时，可以使用`docker-php-ext-install`命令安装或者下载源码编译安装。
4.   nginx转发配置文件中，`fastcgi_pass`可使用`container_name:9000`的方式，也可以使用`宿主机ip:映射端口`的方式转发给fastcgi。
5.   项目配置文件中，mysql和redis的`host`和`port`可使用`宿主机ip`和`映射端口`的方式。注意宿主机使用了DHCP方式加入局域网的ip变化，可考虑手动ip方式。
