# devops-shaik
 
Testing team also there:
------------------------
	developer they will write some code --> testing team will test code
	we need to integrate sonarqube with jenkins

Sonarqube setup:
----------------
https://devopscube.com/setup-and-configure-sonarqube-on-linux/
https://github.com/mastanshaik-kadapa/sonarqube-installation
	some database --> embedded database
if you are going to use your own database, otherwise  it will take embedded database.
	
yum install java* 
yum install java-11-amazon-corretto -y
amazon-linux-extras list
amazon-linux-extras install java-openjdk11

we downloaded zip file
cd /opt sudo wget https://binaries.sonarsource.com/Distribution/sonarqube/sonarqube-7.6.zip
extracted zip
 change ownership with non-root user to /opt/sonarqube-7.6
change RUN_AS_USER as non-root user

[root@ip-10-0-1-156 linux-x86-64]# cat sonar.sh | grep -i ec2-user
RUN_AS_USER=ec2-user
[root@ip-10-0-1-156 linux-x86-64]#
 

/opt/sonarqube-7.6/bin/linux-x86-64/sonar.sh
./sonar.sh start

Default user name and password is admin and admin to login the console.
 https://devopscube.com/setup-and-configure-sonarqube-on-linux/


url: user name and password --> our own database

create database SonarQubedB;
CREATE USER sonar WITH PASSWORD 'Sonar#123';
GRANT CONNECT ON DATABASE SonarQubedB TO sonar;

Now up to db., user, password created. now these details need to integrated with SonarQube.
 

Now connect to postgres database and check the tables.

 
Now the scanner will send the report to sonarqube and data will be stored in postgres DB.

Installation steps of sonarqube scanner.
wget https://binaries.sonarsource.com/Distribution/sonar-scanner-cli/sonar-scanner-cli-4.4.0.2170-linux.zip
unzip sonar-scanner-cli-4.4.0.2170-linux.zip
setup the environment variable to use the sonar-scanner command from any where
export PATH=$PATH:/opt/sonar-scanner/bin
sonar-scanner
now we need to integrate sonar-scanner with sonarqube.
 

Now clone the repository.
git clone https://github.com/mastanshaik-kadapa/sonarqube.git
Cd /root/sonarqube/springboot
Now we required artifacts to scan src folder
Mvn clean install



sonar.jdbc.url=jdbc:postgresql://localhost/sonarqubedb
sonar-scanner -Dsonar.projectKey=hellospringboot \
-Dsonar.projectName=hellospringboot \
-Dsonar.sourceEncoding=UTF-8 \
-Dsonar.sources=src
 
