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
```sql
  mysql -u Name -p
```






[Top](#top)
