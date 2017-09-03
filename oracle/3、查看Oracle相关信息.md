[如何查询oracle数据库中的各种角色](http://www.cnblogs.com/zhanglingfei/p/5970141.html)

### 查看Oracle角色用户及权限
```
1. 查询oracle中所有用户信息
    select user_id, username, DEFAULT_TABLESPACE, ACCOUNT_STATUS,PROFILE from dba_users;
2. 查看当前用户的缺省表空间
    select username,default_tablespace from user_users;
3. 查看当前用户的角色
    select * from user_role_privs;
4. 查看当前用户的系统权限和表级权限
    select * from user_sys_privs
    select * from user_tab_privs
```

### 查看表相关信息
```
1. 查看某表的大小
　　select sum(bytes)/(1024*1024) tablesize from user_segments where segment_name='ZW_YINGYEZ';
2. 查看索引个数和类别
　　select index_name,index_type,table_name from user_indexes order by table_name
3. 查看索引被索引的字段
　　select * from user_ind_columns where table_name='CB_CHAOBIAOSJ201004'
4. 查看索引的大小
　　select sum(bytes)/(1024*1024) as indexsize from user_segments
　　where segment_name=upper('AS_MENUINFO')
```

```
查看oracle版本命令：
    select * from v$version
```