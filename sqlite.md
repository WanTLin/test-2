## sqlite 语法  
- **创建数据库**  
在sqlite3中：  
sqlite3 databasename.db  
退出：.quit  
.dump命令：  
sqlite databasename.db .dump>databasename.sql  
(后面可以将databasename的信息进行回复)  
- **附加数据库**  
ATTACH DATABASE file_name AS database_name;  
(database_name 不能为TEMP和main) 
- **分离数据库**  
DETACH DATABASE database_name  
-  **创建表**  
CREATE TABLE table_name (  
column1 datatype NOT NULL,  
column2 datatype PRIMARY KEY...  
...  
);  
- **删除表**  
DROP TABLE table_name;  
- **INSERT语句**  
**2种语法规则：**  
INSERT INTO table_name (column1,column2...) VALUES (value1,value2...);  
INSERT INTO table_name VALUES (value1,value2,...);  
**从另一张表填充数据：**  
INSERT INTO table_name [(column1,column2,...)] SELECT column1,column2,... FROM sencond_table [WHERE...];  
- **SELECT语句**  
SELECT ( * ) ,column1,column2,... FROM table_name;  
**设置列宽度**  
.width num1,num2,...  
**Schema信息**  
SELECT table_name FROM sqlite_master WHERE type = 'table';  
- **运算符**  
**算术运算符：** +，-，* ，/，%  
**比较运算符：** == / =（皆为比较相等）,!= / <>,>,<,>=,<=,!<,!>  
**逻辑运算符：**  
AND,BETWEEN,IN(与一系列指定表的值)，NOT IN(与一系列指定表的值),  
**EXISTS**:与in的区别，in是在子查询中的列表判断存在与否，exists是loop循环每次判断（）中的条件是否能查询出数值，可以则显示。
LIKE:某值与通配符进行比较  
GLOB:与LIKE相似，但是大小写敏感  
NOT,OR,IS NULL,IS(与=相似),IS NOT(!=),  
||:连接两个不同的字符串  
UNIQUE  
**位运算符**  
&,|,~,<<,>>  
- **WHERE子句**  






