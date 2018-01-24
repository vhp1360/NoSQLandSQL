<div dir=rtl>بنام خدا</div>

###### top
-[Import Dump](#import-dump)
-[Csv Export](#csv-export) 


[top](#top)

### Import Dump
in terminal:
```vala
  impdp UserName/Password@TNSName directory=... dumpfile=....
```
  - if you'd like do that as SYS user:
  ```vala
    impdp \"sys@TnsName as sysdba \" ...
  ```
  
### Csv Export
it's simple:
```vala
  set NLS_LANG=AMERICAN_AMERICA.AL32UTF8
  Set WRAP OFF ECHO OFF
  spool d:\&1.csv;
  Select C1 || ',' || C2 || ',' || C3 || ',' || ... From Tbl Where RowNum> (&1-1) And ROWNUM<= &1;
  spool off;
  exit;
```
  - if you would export many row more than your _RAM_ then you need break down to multiple csv file, 
      then sould use cmd command in windows
  ```vala
      @echo off
      set NLS_LANG=AMERICAN_AMERICA.AL32UTF8
      for /L %%i in (1,1,No) do (
        Set /a b=%%i*1000000  <-- for example
        call sqlplus User/Pass@TnsName @d:\Sql.sql %%b%%
      )
      pause
    ```

