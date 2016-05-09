<html dir='rtl'>
<div dir='rtl' align='right'>بنام خدا</div>

<div dir='rtl' align='right'>نصب و تنظیم پایگاه داده کوچ-بیس</div>

Installation and configuration of Couchbase

OS:CentOS7 Minimal

<div dir='rtl' align='right'>۱-نصب نرم افزار های اولیه</div>

1-fisrt, install some packages

yum update -y --nogpgcheck && yum install java vim mlocate
iptables-services bzip2 gcc gcc-c++ wget policycoreutils
policycoreutils-python selinux-policy selinux-policy-targeted
libselinux-utils setroubleshoot-server setools setools-console
mcstrans-y --nogpgcheck

<div dir='rtl' align='right'>۲-نصب کتابخانه های مورد نیاز اوراکل(که در همین منبع در آموزشی دیگر موجود
است).</div>

2-Installing Oracle if you need(you may fing in OracleOCI file in this
repository).

<div dir='rtl' align='right'>-پس از نصب جاوا و پایتون لازم است که فایل پروفایل مجددا تنظیم شود.</div>

-After installing Java And Python, profile file should be touch.

<div dir='rtl' align='right'>۳-نصب پایتون(چون برای ارتباط با پایگاه داده یکی از انتخاب های خوب می
باشد.)توسط نصب کننده آناکوندا.توجه شود که تانسخه ۴ پایگاه داده کوچ-بیس ،
پایتون۲ قابل استفاده می باشد.</div>

3-Installing Python from Anaconda Installer. be informed,
couchbase1,2,3,4 support Python2.

<div dir='rtl' align='right'>۴-نسخه مورد نظر پایگاه داده
<a href="http://www.couchbase.com/nosql-databases/downloads">کوچ-بیس</a> را تهیه
کرده</div>

4-download approperiate
[couchbase](http://www.couchbase.com/nosql-databases/downloads) version
and install.

<div dir='rtl' align='right'>۵-پس از نصب کوچ-بیس باید پورت های مورد نیاز را در دیواره آتش(جدول آدرس
ها) باز نمایید</div>

5-after installation, you should open needed ports in iptables.

</html>
