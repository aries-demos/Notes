### 导入导出

```
exp ums/ums1234@ORCL file=/opt/hy-ums.dmp owner=ums
导入：
复制文件到 docker容器
imp ums_dev/ums_dev jdbc:oracle:thin:@localhost:1521:XE  file=expdat.dmp ignore=y
imp ums_dev/ums_dev@XE  file=c:\orabackup\hkbfull.dmp log=c:\orabackup\hkbimp.log full=y

```
#### 导出
```
1、只导出表结构
本地： 
exp ums/ums1234@ORCL file=ums_pingan.dmp log=ums_pingan.log owner=ums rows=n
远程： 
exp ums_pingan/ums_pingan jdbc:oracle:thin:@10.10.73.206:1521:umpay file=ums_pingan.dmp log=ums_pingan.log owner=ums rows=n
```