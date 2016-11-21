<div dir="rtl">بنام خدا</div>

* Security
	1. Data Buckets|Edit|Access Control|Standard Port->EnterPassword
		1. in Python SDK for Connection
		```python
			from couchbase.bucket import Bucket
			bucket = Bucket('couchbases://IP/default',password='BucketPassword')
		```
	2. put Couchbase beside of Nginx
	```vala
		server {
			listen 38091 ssl;
			client_max_body_size 21m;                            
			ssl_certificate /Path/nginx.crt;
			ssl_certificate_key /Path/nginx.key;
			ssl_session_cache   shared:SSL:10m;
			ssl_session_timeout 10m;
			ssl_protocols  SSLv2 SSLv3 TLSv1;
			ssl_ciphers  ALL:!ADH:!EXPORT56:RC4+RSA:+HIGH:+MEDIUM:+LOW:+SSLv2:+EXP;
			ssl_prefer_server_ciphers   on;
			location / { #/couchbase/ {
				proxy_pass http://localhost:8091; #couchbase_gateway;
				#      rewrite ^/couchbase/(.*)$ /$1 break;
				#      proxy_redirect http://localhost:8091/ $scheme://$host/couchbase/;
				proxy_pass_header       Accept;
				proxy_pass_header       Server;
				proxy_http_version      1.1;
				keepalive_requests      1000;
				keepalive_timeout       360s;
				proxy_read_timeout      360s;
				proxy_set_header Upgrade $http_upgrade;
				proxy_set_header Connection $connection_upgrade;
			}
		}
	```
	3. SSL/TLS connection for SDKs
		+ 3.1.Security|Root Certifies-> save certficate in client machine
		```python
			from couchbase.bucket import Bucket
			bucket = Bucket('couchbases://IP/default?certpath=/Path/cert.pem')
		```
		+ 3.2.if you also have port password
		```python
			from couchbase.bucket import Bucket
			bucket = Bucket('couchbases://IP/default?certpath=/Path/cert.pem',password='PortPasswod!')
		```
	4. IPTABLES issues:
	```
	  -A INPUT -p tcp -m tcp -m state --state NEW,RELATED,ESTABLISHED -m multiport --dports\
		8093,11207,11209:11211,11214,11215,18091,18092,4369,21100:21199 -j ACCEPT
	```
	5. Retrive Certificate:
		+ 5.1.in None SSL:
		```vala
			curl –X GET  -u adminName:adminPassword http://localHost:Port/pools/default/certificate > ./<certificate_name>
			for example:
			curl http://10.5.2.54:8091/pools/default/certificate > clusterCertificate
			or
			wget http://10.5.2.54:8091/pools/default/certificate -O clusterCertificate
		```
		+ 5.2.in SSL Mode:
		```vala
			curl --cacert clusterCertificate https://10.5.2.54:18091/pools/default
			wget --ca-certificate clusterCertificate  https://10.5.2.54:18091/pools/default -O outpu
		```

<div dir="rtl"></div>
<div dir="rtl"></div>
<div dir="rtl"></div>
<div dir="rtl"></div>
<div dir="rtl"></div>
<div dir="rtl"></div>
<div dir="rtl"></div>



