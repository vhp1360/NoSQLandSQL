<div dir="rtl">بنام خدا</div>

<div dir="rtl">تغییر واترمارک</div><br/>
Change Water-Mark values<br/>
*cbepctl* _IP:11210_ *-b* _BucketName_ *-p* _Password_ *set* *flush_param* _{*mem_low_wat*|*mem_high_wat*|*pager_active_vb_pcnt*}_ _NewValue_

In addition, generally speaking, Couchbase works hard to keep as much of the data as possible in memory including replicas. This benefits you in that you'll have faster failover in the event of failure. 

http://developer.couchbase.com/documentation/server/4.1/developer-guide/raw-append-prepend.html#story-h2-2<br/>

Currently there is a hard limit of 10,000 concurrent key-value connections to any cluster node. This effectively means a limit of 10,000 SDK “Bucket” objects.


<div dir="rtl"></div>
<div dir="rtl"></div>
<div dir="rtl"></div>
