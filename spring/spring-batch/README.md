### spring-batch是什么
官网介绍：一款轻量的、全面的批处理框架，用于开发强大的日常运营的企业级批处理应用程序。

框架主要有以下功能：

```
Transation managerment（事务管理）
Chunk based processing（基于块的处理）
Declarative I/O（声明式的输入输出）
Start/Stop/Restart（启动/停止再启动）
Retry/Skip（重试/跳过）
```

### 框架全貌
框架一共有4个角色：

```
JobLauncher是任务启动器，通过它来启动任务，可以看做是程序的入口。
Job代表这一个具体的任务。
Step代表一个具体的步骤。
JobRepository是存储数据的地方，可以看做是一个数据库的接口，在任务执行的时候需要通过它来记录任务状态等信息。
```

更多的使用介绍及Demo：[大数据批处理框架 Spring Batch全面解析](http://blog.csdn.net/huojiao2006/article/details/54287098)