Oracle的安装还是挺麻烦的。然而使用Docker，可以简单、方便的搭建Oracle环境

[阿里云Docker镜像地址](https://dev.aliyun.com/detail.html?spm=5176.1972343.2.6.myJcM9&repoId=1969)

### 安装步骤
```
1、首先在docker环境下载镜像
docker pull registry.cn-hangzhou.aliyuncs.com/helowin/oracle_11g
2、启动容器(启动花了一分钟唉，有点慢哦)
docker run -d --name oracle11g -p 1521:1521  registry.cn-hangzhou.aliyuncs.com/helowin/oracle_11g

```
如果想将数据文件映射到主机方便管理，可以在启动容器时添加参数
-v  /opt/data/oracle：/home/oracle/app/oracle/oradata/

/home/oracle/app/oracle/oradata/为容器数据文件位置

### 配置sqlplus使用oracle
一般有客户端工具连接Oracle进行使用。但有些场景比如权限分配等管理员操作，使用sqlplus比较方便。

```
Linux下Oracle环境变量设置
编辑.bashrc 或者 .bash_profile，添加如下：
export ORACLE_SID=helowin
export ORACLE_HOME=/home/oracle/app/oracle/product/11.2.0/dbhome_2
export PATH=$ORACLE_HOME/bin:$PATH
这样就可以在oracle用户下输入sqlplus进入命令行客户端啦。
```

注意：刚启动的容器没有用户名和密码，system的用户也不能使用（不知道为什么）。刚开始很疑惑怎么使用？

[Oracle默认的用户及密码](http://blog.csdn.net/catchmybreath123/article/details/30744099)

```
不登陆到数据库，使用管理员身份连接。然后修改密码。
sqlplus /nolog
conn /as sysdba
alter user system identified by manager
```



OK,现在可以正常使用Oracle数据库服务啦。具体使用的一些命令和注意点见下章节。

### 额外的操作
1、修改实例名
```
登陆数据库，查看实例名
select instance from v$thread;
查看环境变量中的实例名
echo $ORACLE_SID
```
好了，修改实例名还是挺麻烦的，而且容易出错，所以我们还是学学怎么在Oracle环境的基础上新建实例吧。

好吧，创建实例也好像很麻烦，能用就好了，太运维的东西先扔下吧。