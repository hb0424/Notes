# Oracle
## 参数文件
### 数据库参数文件
init<ORACLE_SID>.ora. After Oracle 9i: spfile<ORACLE_SID>.ora.  
Windows Path: %ORACLE_HOME%\DATABASE  
Linux Path: $ORACLE_HOME/dbs  
spefic pfile when start up oracle instance: pfile=filepath  
convert PFILE to SPFILE: Create spfile
ALTER SYSTEM command can modify SPFILE only. and only ALTER SYSTEM command can modify SPFILE.
#### 查看参数
SELECT value FROM "GV$PARAMETER" WHERE name = 'db_block_size';  
SELECT name, value FROM "GV$PARAMETER";  
show PARAMETER db_block_size;  
show parameter spfile;
#### 设置SPFILE中的参数值
Alter system set parameter=value <commnet='text'> <deferred> <scope=memory|spfile|both> <sid='sid|*'> <container=current|all>  
deffered: become effective for the session later, not effective for current session  
    The parameter must to be deferred:  
    SELECT name, value, ISSYS_MODIFIABLE FROM "GV$PARAMETER" WHERE ISSYS_MODIFIABLE = 'DEFERRED';  
