# tomcat_aws
tomcat on aws 

Download tomcat package from https://tomcat.apache.org/download-80.cgi
Copy the link tar.gz 

![image](https://user-images.githubusercontent.com/10364043/228803716-3cb648b2-7f9c-4320-a200-f2ff8c20b870.png)

Login instance 
$ sudo su - 
$ cd /opt 
$ wget https://dlcdn.apache.org/tomcat/tomcat-8/v8.5.87/bin/apache-tomcat-8.5.87.tar.gz 

$ tar -zvxf  apache-tomcat-8.5.87.tar.gz 
$ cd apache-tomcat-8.5.87/bin

--to check running or not 
$ ps -ef | grep tomcat 

to see permission 
$ ls -ltr 
no full permission on startup.sh 

![image](https://user-images.githubusercontent.com/10364043/228806113-c0334f66-c594-4fb2-8e7e-8ee15a6ca609.png)

to add permission 

$ chmod +x startup.sh 
$ chmod +x shutdown.sh 
$ ln -s /opt/apache-tomcat-8.5.87/bin/startup.sh /usr/local/bin/tomcatup 
$ ln -s /opt/apache-tomcat-8.5.87/bin/shutdown.sh /usr/local/bin/tomcatdown

If Jenkins installed on same instance. Port 8080 is busy. 
Add 9090 to redhat instance security group 

![image](https://user-images.githubusercontent.com/10364043/228812062-13d33a91-0ee3-4a04-8674-544678152523.png)


Need to change port for Tomcat
To change the default port of Apache Tomcat from 8080 to 9090 on an EC2 instance running Red Hat, you need to follow these steps:
1- Open the server.xml file located in the Tomcat configuration directory. The default location for this file is /usr/share/tomcat/conf/:

2- Find the Connector element that defines the HTTP/1.1 connector, which should look something like this: 

<Connector port="8080" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />
           
          
3- Change the port attribute to 9090: 

<Connector port="9090" protocol="HTTP/1.1"
           connectionTimeout="20000"
           redirectPort="8443" />

4- Save and close the server.xml file.
5- Restart Tomcat to apply the changes:

$ sudo service tomcat restart
  
$ sudo vi /usr/share/tomcat/conf/server.xml
$ tomcatup 

$ find / -name context.xml 
vi /opt/apache-tomcat-8.5.87/webapps/host-manager/META-INF/context.xml
vi /opt/apache-tomcat-8.5.87/webapps/manager/META-INF/context.xml

![image](https://user-images.githubusercontent.com/10364043/228821372-82685c79-cbb3-4f69-9bec-64fbebabec4e.png)

$ tomcatdown
$ tomcatup 

Restart 

![image](https://user-images.githubusercontent.com/10364043/228821697-dff6b9a4-6ebd-472c-95cb-d818d8a2e1ff.png)


To create a user in Tomcat 8 running on Red Hat on an AWS instance, you can follow these steps:
1- Open the tomcat-users.xml file located in the conf directory of the Tomcat installation:

$ sudo vi /usr/share/tomcat/conf/tomcat-users.xml

2- Add a new user to the tomcat-users.xml file. For example, 
to create a user with the username myuser and password mypassword 
and assign them the manager-gui and admin-gui roles, add the following lines:

$ <user username="myuser" password="mypassword" roles="manager-gui,admin-gui"/>

3- Save and close the tomcat-users.xml file.

4- Restart Tomcat to apply the changes:

Done. 
