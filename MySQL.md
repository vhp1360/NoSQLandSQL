<div dir='rtl'>بنام خدا</div>

###### top

- [Installation](#installation)
- [Password Recovery](#password-recovery)
- [Some Codes](#some-codes)


[Top](#top)

### Installation
- if you faced InnoDB issue like: '[ERROR] InnoDB: Upgrade after a crash is not supported', \ 
    'InnoDB: Plugin initialization aborted with error Generic error' the solution is removing _ib\_logfile0,ib\_logfile1_ or \
    may _aria\_log\_control_
    


[Top](#top)
### Password REcovery
1- in /etc/my.cnf add `skip-grant-tables` line

2- 
```vim
      service mysqld restart
      mysql -u root
      use mysql
      UPDATE mysql.user set password = PASSWORD('your_new_password') where user = 'root' and host = 'localhost';
      FLUSH PRIVILAGES;
      exit;
```


[Top](#top)
### Some Codes
- login :
```vala
  mysql -u Name -p
```
- MetaData:
  1- DataBases, Schema,Tables
  ```vala
      SHOW {DATABASES | SCHEMAS | TABLES};
      SHOW TABLES;
  ```
  2- Column Names
  ```vala
    DESCRIBE my_table;
    SELECT COLUMN_NAME FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_SCHEMA = 'my_database' AND TABLE_NAME = 'my_table';
  ```
  3- 
  
- Use File:
```vala
  mysql> source /Path/to/File
```
- Create USER and Grant:
```vala
  mysql> CREATE USER 'UserName'@'localhost' IDENTIFIED BY 'Password';
  mysql> GRANT ALL PRIVILEGES ON DatabaseName.* TO 'UserName'@'localhost' WITH GRANT OPTION;
  FLUSH PRIVILEGES;
```
- Select
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
  3- 


[Top](#top)
