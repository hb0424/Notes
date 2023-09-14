# Oracle
## 参数文件
### 数据库参数文件
init<ORACLE_SID>.ora. after Oracle 9i:spfile<ORACLE_SID>.ora.  
#### 查看参数
SELECT value FROM "GV$PARAMETER" WHERE name = 'db_block_size';  
SELECT name, value FROM "GV$PARAMETER";  
show PARAMETER db_block_size;  
