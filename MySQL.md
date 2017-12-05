<div dir='rtl'>بنام خدا</div>

###### top

- [Installation](#installation)
- [Password Recovery](#password-recovery)
- [Some Codes](#some-codes)
    - [Login](#login)
    - [MetaData](#metadata)
    - [Use File](#use-file)
    - [Create USER and Grant](#create-user-and-grant)
    - [SELECT](#select)


[Top](#top)

### Installation
- if you faced InnoDB issue like: '[ERROR] InnoDB: Upgrade after a crash is not supported', \ 
    'InnoDB: Plugin initialization aborted with error Generic error' the solution is removing _ib\_logfile0,ib\_logfile1_ or \
    may _aria\_log\_control_
    


[Top](#top)
### Password Recovery
1- in /etc/my.cnf add `skip-grant-tables` line

2- 
```vim
	service mysqld restart
	mysql -u root
	mysql> use mysql
	mysql> UPDATE mysql.user set password = PASSWORD('your_new_password') where user = 'root' and host = 'localhost';
	mysql> FLUSH PRIVILAGES;
	mysql> exit;
```


[Top](#top)
### Some Codes
- ###### login:
```vala
	mysql -u Name -p
```
- ###### MetaData:

  1- DataBases, Schema,Tables
  ```vala
		mysql> \u DataBaseName;
		mysql> ALTER DATABASE dbname CHARACTER SET utf8 COLLATE utf8_general_ci;
		mysql> ALTER TABLE tablename CHARACTER SET utf8 COLLATE utf8_general_ci;
		mysql> ALTER TABLE `db_table_name` DEFAULT CHARACTER SET utf8 COLLATE utf8_general_ci;
		mysql> SHOW {DATABASES | SCHEMAS | TABLES};
		mysql> SHOW TABLES;
  ```
  2- Column:
  ```vala
    mysql> DESCRIBE my_table;
    mysql> SELECT COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_SCHEMA = 'my_database' AND TABLE_NAME = 'my_table';
    mysql> ALter TAble TablaName Modify Column ColumnName1 ..., Modify Column ColumnName ...  
  ```
  3- Find Keys:
  ```vala
    mysql> SELECT
        CONCAT(table_name, '.', column_name) AS 'foreign key',
        CONCAT(referenced_table_name, '.', referenced_column_name) AS 'references',
        constraint_name AS 'constraint name'
    FROM
        information_schema.key_column_usage
    WHERE
        referenced_table_name IS NOT NULL;
  ```
4- 


- ###### Use File:
```vala
  mysql> source /Path/to/File
  mysql> load data local infile '/Path/to/File.csv' into table TableName Fields Terminated by ',' Enclosed by '"' \
					Line Terminated by '\n' Ignore No. Lines (ColName1,ColName2,...)
```
- ###### Create USER and Grant:
```vala
  mysql> CREATE USER 'UserName'@'localhost' IDENTIFIED BY 'Password';
  mysql> CREATE USER 'UserName'@'IP' IDENTIFIED BY 'Password';
  mysql> CREATE USER 'UserName'@'%' IDENTIFIED BY 'Password';
  mysql> GRANT ALL PRIVILEGES ON DatabaseName.* TO 'UserName'@'localhost' WITH GRANT OPTION;
  FLUSH PRIVILEGES;
```
- ###### Select:

  1- Top:
  ```vala
    Select * from TableName Limit No.  Offset No.;
  ```
  2- RowNumber:
  ```vala
    SELECT *   -- <-- pick any columns here from your table, if you wanna exclude the RowNumber
    FROM (SELECT ROW_NUMBER OVER(ORDER BY ID DESC) RowNumber, * 
          FROM Reflow  
          WHERE ReflowProcessID = somenumber) t
    WHERE RowNumber >= 20 AND RowNumber <= 40  
  ```
  3- Join:
  ```vala
    Select ... From T1 [any Type of] Join (T2,..,Tn) ON T1...=T2... And T1...=....
  ```
[Top](#top)
