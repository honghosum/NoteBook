## 启动MySQL

#### 启动服务
    
    cmd > net start mysql80
    
    或在任务管理器中，到服务选项卡里找到MySQL80，右击开始
    
#### 使用MySQL
    
    cmd > mysql -hlocalhost -uroot -proot
    
    -h表示服务器名，localhost表示本地
    
    -u为数据库用户名，root是mysql默认用户名
    
    -p为密码，如果设置了密码，可直接在-p后直接输入
    
#### 导入.csv

    启动客户机读取文件权限

    cmd > set global local_infile = 1
    
    修改数据上传/导出目录限制
    
    在\MySQL\MySQL Server 8.0\bin目录下，打开my.ini配置文件
    
    找到secure-file-priv，用#注释原有目录，在下面添加secure-file-priv=""
    
    **注意**
