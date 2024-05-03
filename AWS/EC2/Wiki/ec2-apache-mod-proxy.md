# EC2 mod_proxy 설정

## Web 인스턴스에 Apache 설치
~~~
sudo yum update
sudo yum install httpd
~~~
<br/>

> 아래 파일을 수정한다.
~~~
sudo vi /etc/httpd/conf/httpd.conf
~~~
<br/>

>아래 내용에서 [ ] 부분을 해당 IP주소에 맞게 수정한다.
~~~
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_http_module modules/mod_proxy_http.so

<VirtualHost *:80>
        ServerName [WAS 인스턴스 IP주소]
# 포워드 Proxy 경우 On Reverse Proxy Off
        ProxyRequests Off
# HTTP 호스트가 받은 HTTP 요청을 Proxy 요청시 사용 Reverse 경우 On으로 해야함
        ProxyPreserveHost On

        ProxyPass / http://[WAS 인스턴스 IP주소]:8080/
        ProxyPassReverse / http://[WAS 인스턴스 IP주소]:8080/
</VirtualHost>
~~~
<br/>

~~~
<Location / >
    ProxyPass / http://10.0.2.108:8080/
    ProxyPassReverse / http://10.0.2.108:8080/
</Location>
<Location / >
    ProxyPass / http://10.0.3.144:8080/
    ProxyPassReverse / http://10.0.3.144:8080/
</Location>
~~~

