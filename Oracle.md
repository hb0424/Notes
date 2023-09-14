# Oracle
## 参数文件
### 数据库参数文件
init<ORACLE_SID>.ora. After Oracle 9i: spfile<ORACLE_SID>.ora.  
Windows Path: %ORACLE_HOME%\DATABASE  
Linux Path: $ORACLE_HOME/dbs  
#### 查看参数
SELECT value FROM "GV$PARAMETER" WHERE name = 'db_block_size';  
SELECT name, value FROM "GV$PARAMETER";  
show PARAMETER db_block_size;  
