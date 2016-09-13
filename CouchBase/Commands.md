<div dir="rtl">بنام خدا</div>

<div dir="rtl">تغییر واترمارک</div><br/>
Change Water-Mark values<br/>

    *cbepctl* _IP:11210_ *-b* _BucketName_ *-p* _Password_ *set* *flush_param* _{*mem_low_wat*|*mem_high_wat*|*pager_active_vb_pcnt*}_ _NewValue_

In addition, generally speaking, Couchbase works hard to keep as much of the data as possible in memory including replicas. This benefits you in that you'll have faster failover in the event of failure. 

    http://developer.couchbase.com/documentation/server/4.1/developer-guide/raw-append-prepend.html#story-h2-2<br/>

Currently there is a hard limit of 10,000 concurrent key-value connections to any cluster node. This effectively means a limit of 10,000 SDK “Bucket” objects.

-create Index

    create primary index `From_Account` on `ShomaraDB` USING VIEW;
    

-View Sample: Bank Transaction, get report each Account who sender or receiver

    function(meta,doc){
      emit(doc.From,doc.DepositeSender)
      emit(doc.To  ,doc.DepositeReceiver)

-View Sample: State of Transactions for each day, each Account

     function (doc, meta) {
      var docTime=doc.Time.split(" ")[0]
          
      emit([docTime,doc.From_Account],parseInt(doc.depositofReceiver))
      emit([docTime,doc.From_Account],parseInt(doc.Transfered_Credit))
      emit([docTime,doc.From_Account],parseInt(doc.depositofSender))
    }

-View Sample: Today Transaction for Account

    function (doc, meta) {
      var today = new Date();
      var dd = today.getDate();
      var mm = today.getMonth()+1; //January is 0!
      var yyyy = today.getFullYear();
      if(dd<10) { dd='0'+dd } 
      if(mm<10) { mm='0'+mm } 
      today = yyyy+"-"+mm+'-'+dd;
        
      var docTime=doc.Time.split(" ")[0]
        
      if (docTime==today) {
        emit(doc.From_Account, [doc.Time,doc.index,doc.depositofReceiver,
          doc.Transfered_Credit,doc.doc_type,doc.To_Account,doc.depositofSender,
          doc.state]);
      
      }
    }


<div dir="rtl"></div>
<div dir="rtl"></div>
<div dir="rtl"></div>
