## sqlite 语法  
- **创建数据库**  
在sqlite3中：  
sqlite3 databasename.db  
退出：.quit  
.dump命令：  
sqlite databasename.db .dump>databasename.sql  
(后面可以将databasename的信息进行回复)  
- **附加数据库**  
ATTACH DATABASE file_name AS database_name  
(database_name 不能为TEMP和main)  

