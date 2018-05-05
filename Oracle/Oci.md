<div dir='rtl' align='right'><h1>بنام خدا</h1></div>

#### installing oracle library withou oracleclient

<div dir='rtl' align='right'>نحوه نصب کتابخانه های لازم پایگاه داده اوراکل بدون نیاز به نصب آن</div>

Oracle oci library installation without installing oracle DB.

<div dir='rtl' align='right'> ابتدا بسته های مورد نظر را از مسیر دریافت نمایید و نصب نمایید</div>

first download required packages from [here](http://www.unixmen.com/install-oracle-client-centos/) link, so install them
```vala
  yum install -y oracle-instantclient*
```
<div dir='rtl' align='right'>میانبرهای زیر را ایجاد نمایید(البته باید بصورت خودکار ایجاد شده باشند)</div>

make below soft links(also they should be created while installaion).
```vala
  ln -s /usr/lib/oracle/12.1/client64/lib/libclntsh.so.12.1 /usr/lib/oracle/12.1/client64/lib/libclntsh.so 
  ln -s /usr/lib/oracle/12.1/client64/lib/libocci.so.12.1 /usr/lib/oracle/12.1/client64/lib/libocci.so 
  mkdir -p /usr/lib/oracle/12.1/client64/rdbms
  ln -s /usr/include/oracle/12.1/client64 /usr/lib/oracle/12.1/client64/rdbms/public 
```
<div dir='rtl' align='right'>حال لازم است که آدرس های جدید را به نمایه(پروفایل) خوداضافه نمایید.</div>

Now, add below addresses to profile file.
```vala
  export ORACLE_HOME=/usr/lib/oracle/12.1/client64 
  export LD_LIBRARY_PATH=$ORACLE_HOME/lib 
```
<div dir='rtl' align='right'>جهت اتصال به اوراکل می توانید از مثال زیر کمک بگیرید. توجه شود که باید فایل ojdbcX.jar مناسب با نسخه پایگاه خود را نیز تهیه کرده و در مسیر اوراکل (که در بالا تعریف کرده اید) قرار دهید.</div>

use below sapmle to connect to oracle, please attemtion for below stringconnection you need ojdbcX.jar file that matched with your oracle version.
```vala
oracle:thin:userid/password@IP:PORT/SID
```


