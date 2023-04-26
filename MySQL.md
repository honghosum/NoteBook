## 启动MySQL

### 启动服务
    
    cmd > net start mysql80
    
    或在任务管理器中，到服务选项卡里找到MySQL80，右击开始
    
### 登录MySQL
    
    cmd > mysql -hlocalhost -uroot -proot
    
    -h表示服务器名，localhost表示本地
    
    -u为数据库用户名，root是mysql默认用户名
    
    -p为密码，如果设置了密码，可直接在-p后直接输入
    
## 导入.csv

### 启动客户机读取文件权限
    
    重新登录MySQL
    
    cmd > mysql --local-infile=1 -hlocalhost -uroot -proot
    
    mysql > set global local_infile = 1
    
    查看权限是否打开
    
    mysql > show variables like 'local_infile';
    
    如果未在mysql内打开，则会出现ERROR 3948 Loading data is disabled; this must be enabled on both client and server sides
    
    如果未在登录MySQL时打开，则会出现ERROR 2068 LOAD DATA LOCAL INFILE file request rejected due to restrictions on access
    
### 修改数据上传/导出目录限制
    
    在\MySQL\MySQL Server 8.0\bin目录下，打开my.ini配置文件
    
    找到secure-file-priv，用#注释原有目录，在下面添加secure-file-priv=""
    
    在修改配置文件后，重启MySQL80服务即可
    
    如果出现“本地计算机上的MySQL80服务启动后停止。某些服务在未由其他服务或程序使用时自动停止”
    
    则用记事簿再打开my.ini，另存为编码选择ANSI，覆盖当前的my.ini即可
    
    查看限制是否已修改
    
    mysql > show variables like '%secure%';
    
    如果未修改，则会出现ERROR 1290 The MySQL server is running with the --secure-file-priv option so it cannot execute this statement
    
### 导入文件

    先预处理csv文件，用Notepad++打开文件，编码-转为UTF8编码-保存
    
    否则会出现ERROR 1300 Invalid utf8mb3 character string

    mysql > use [database];
            load data local infile './path/doc.csv'
            into [table]
            fields terminated by ','
            lines terminated ny '\n'
            ignore 1 rows
            ([field1], [field2], [field3], [field4], ...);
    
    fields terminated by 表示列之间以什么符号为分隔符
    
    lines terminated by 表示行之间以什么符号为分隔符，通常为换行符
    
    ignore 1 rows 如果已在mysql中定义表和它的各个字段，忽略1行则是忽略csv中的表头
