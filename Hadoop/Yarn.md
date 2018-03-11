<div dir=rtl>بنام خدا</div>

- [Tips]


### Tips

- `yarn logs --applicationId <application_id_of_your_job>`
###### - in [_Hadoop Mapper is failing because of “Container killed by the ApplicationMaster”_](https://stackoverflow.com/questions/30533501/hadoop-mapper-is-failing-because-of-container-killed-by-the-applicationmaster) should use below config in _yarn-site.xml_ :
```xml
  <property>
   <name>yarn.nodemanager.vmem-check-enabled</name>
   <value>false</value>
   <description>Whether virtual memory limits will be enforced for containers</description>
  </property>
  <property>
   <name>yarn.nodemanager.vmem-pmem-ratio</name>
   <value>4</value>
   <description>Ratio between virtual memory to physical memory when setting memory limits for containers</description>
  </property>
```
