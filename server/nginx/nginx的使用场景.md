nginx有很多的第三方模块。但最基本的一些功能还是很有必要先搞清楚。

### nginx能做什么？
- 反向代理
- 负载均衡
- Http服务器（包含动静分离）
- 正向代理

#### 一、反向代理
反向代理：就是以代理服务器来接受Internet上的连接请求，并将服务器上得到的结果返回Internet上请求的客户端。

以下配置即可实现反向代理：

```
server{
	listen	80;
	server_name	localhost;
	client_max_body_size	1024M;
	
	location / {
		proxy_pass	http://localhost:8080;
		proxy_set_header Host	$host:$server_port;
	}
}
```

#### 二、负载均衡
就是分摊到多个操作单元上进行执行，例如Web服务器、FTP服务器、企业关键应用服务器和其它关键任务服务器等，从而共同完成工作任务。即：将请求根据规则随机分发到指定的服务器上处理。

nginx目前支持自带3中负载均衡策略，还有2种常用的第三方策略。

1、RR（默认）：每个请求按照时间顺序逐一分配到不同的后端服务器，如果后端服务器down掉，能自动剔除。

```
upstream test{
	server	localhost:8080;
	server 	localhost:8001;
}
server{
	listen	81;
	server_name	lcoalhost;
	client_max_body_size	1024M;
	
	location / {
		proxy_pass	http://test;
		proxy_set_header	Host	$host:$server_port;
	}
}
```

如果有某台服务器处于不能访问（down），nginx会自动判断服务器的状态。不会跳转到挂掉的服务器。

2、权重：指定轮训几率，weight和访问比率成正比，用于后端 服务器性能不均的情况。

```
upstream test{
	server	localhost:8080	weight=9;
	server 	localhost:8001	weight=1;
}
```

3、ip_hash:同一个ip取hash分发到指定的服务器，多次请求会指向同一服务器，可以解决双机session的问题。

```
upstream test{
	ip_hash ;
	server	localhost:8080	weight=9;
	server 	localhost:8001	weight=1;
}
```

4、fair（第三方）:按后端服务器的响应时间分配请求，响应时间短的优先分配。

```
upstream test{
	fair ;
	server	localhost:8080	weight=9;
	server 	localhost:8001	weight=1;
}
```

5、url_hash(第三方):类似ip_hash,后端服务器为缓存时比较有效。

#### 三、Http服务器
nginx本身也是一个静态资源的服务器，当只有静态资源的时候，就可以使用nginx来做服务器。

动静分离:

```

```

#### 四、正向代理
