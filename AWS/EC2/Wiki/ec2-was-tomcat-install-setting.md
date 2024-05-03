# EC2 Was Server Tomcat 설치 및 환경변수 설정

<https://tomcat.apache.org/download-80.cgi> 에서 tar.gz 다운로드 링크 복사

> wget으로 tar파일 가져오기
~~~
wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.81/bin/apache-tomcat-8.5.81.tar.gz
~~~
<br/>

>tar.gz 압축 해제
~~~
tar xvfz apache-tomcat-8.5.81.tar.gz
~~~
<br/>

>압축 해제된 파일 옮기기
~~~
mv apache-tomcat-8.5.81 /usr/local/tomcat8.5
~~~
<br/>

>설치 가능한 자바 확인 및 설치
~~~
sudo yum list | grep jdk
sudo yum install java-1.8.0-openjdk
#javac 설치
sudo yum install java-1.8.0-openjdk-devel.x86_64
~~~
<br/>

>환경 변수 설정할 경로 찾기
~~~
which java
-> /usr/bin/java
readlink -f /usr/bin/java
-> /usr/lib/jvm/java-1.8.0-openjdk-1.8.0.332.b09-1.amzn2.0.2.x86_64/jre/bin/java
~~~
<br/>

>환경 변수 설정
~~~
sudo vi /etc/profile

#아래 내용 추가
export JAVA_HOME=/usr/lib/jvm/java-1.8.0-openjdk-1.8.0.332.b09-1.amzn2.0.2.x86_64
export PATH=$PATH:$JAVA_HOME/bin
export CLASSPATH=$JAVA_HOME/jre/lib:$JAVA_HOME/lib/tools.jar

export CATALINA_HOME=/usr/local/tomcat8.5
:wq!

#수정한 내용 적용
source /etc/profile 
~~~
<br/>