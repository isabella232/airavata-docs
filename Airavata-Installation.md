
## Install Apache Airavata

<br><b>Click your option;</b></br>

[<button type="button" style="color:#3232ff;text-align:center;font-weight:bold;background-color:darkgray;width:200px;border-radius:4px">Airavata Prerequisites</button>](#Airavata) &nbsp; &nbsp; &nbsp;
[<button type="button" style="color:#3232ff;text-align:center;font-weight:bold;background-color:darkgray;width:200px;border-radius:4px">Airavata on CentOS 7</button>](#AiravataCent) <br></br>


### <h3 id="Airavata">General Prerequisites</h3>
1. JAVA 8
	- Java installation on CentOS, Mac, Windows, etc.. - <a href="https://docs.oracle.com/javase/8/docs/technotes/guides/install/install_overview.html" target="_blank">Oracle JAVA Installation</a>
2. RabbitMQ
	- <a href="https://www.rabbitmq.com/download.html" target="_blank">Download the RabbitMQ Binary</a><br>Select the download file as per the operating system of your machine/server.
	- Same link has installing guide documentation as well. E.g.:<a href="https://www.rabbitmq.com/install-standalone-mac.html" target="_blank">MAC Installation Guide</a>
	- For  detailed information on getting RabbitMQ started, stopped, etc please visit <a href="https://www.rabbitmq.com/documentation.html" target="_blank">RabbitMQ Documentation</a>
3. Maven
	- <a href="http://maven.apache.org/download.cgi" target="_blank">Download Maven</a> (java based code building tool).
4. MySQL Database

### <h3 id="AiravataCent">Airavata Installation on CentOS 7</h3>
<b>NOTE: Airavata installation on other operating systems are similar with minor changes.</b></br>
#### Pre-Installations
1. CentOS 7 Default open JDK 1.8.0. (minimum) is sufficient. Use "yum search jdk" to find available versions. Verify versions using "javac -version". Be sure to install the developer version.
<pre><code>yum install java-1.8.0-openjdk-devel.x86_64</code></pre>
2. Download RabbitMQ binary for CentOS 7
<a href="https://www.rabbitmq.com/install-generic-unix.html" target="_blank">Download RabbitMQ Binary for CentOS</a><br>
3. Prerequisite for RabbitmQ Erlang can be installed using yum
<pre><code>yum install erlang</code></pre>
4. Unzip the downloaded RabbitMQ tar file into a folder in your local machine.
<pre><code>tar -xvf rabbitmq-server-mac-standalone-3.4.1.tar.gz</code></pre>
5. Start the RabbitMQ server in the bin folder using;
 <pre><code>./sbin/rabbitmq-server start</code></pre>
6. Install Maven using yum install. ((install the latest maven 3.3.9. Default Maven default of centOS 7).
<pre><code>yum install maven</code></pre>
7. Install MySQL database
<pre><code>yum install mariadb-server</code></pre>
8. Start maria DB with;
<pre><code>systemctl start mariadb</code><pre>
9. While maria DB is running run
<pre><code>mysql _secure_installation</code></pre>
When executing above it will ask you for root password; provide it.
10. Now login as the root user providing the password you gave above.
10. Create databases required for Airavata
<pre><code>create database app_catalog;</code></pre>
<pre><code>create database experiment_catalog;</code></pre>
<pre><code>create database replica_catalog;</code></pre>
<pre><code>create database credential_store;</code></pre>
<pre><code>create database workflow_catalog;</code></pre>
11. Grant permission to these databases for a new user which would be used by Airavata<br>
Command syntax: 
<pre><code> grant all privileges on &#60;DB-Name&#62;&#46;&#x204E; to '&#60;username&#62;'@'%' identified by '&#60;password&#62;'; </code></pre>
E.g.: 
<pre><code>grant all privileges on app_catalog&#46;&#x204E; to 'airavata'@'%' identified by 'airavata';</code></pre>
<br>
NOTE: Grant permission to every databased created above. % can be replaced by  'localhost' (if DB is also in the same server as airavata). If DB is in a different server give the server name.
<br>

#### Airavata Installation
1. Create a folder in your local machine (E.g.: mkdir LocalAiravata).<br>
2. Clone the master source (If you have not taken a clone prior) code from github to the created folder.<br>
<pre><code>git clone https://github.com/apache/airavata.git</code></pre>
3. After cloning is completed, build the source code by executing following maven command (In LocalAiravata directory you made);
<pre><code>mvn clean install</code></pre>
Hint: To avoid tests (recommended for first time users) use
<pre><code>mvn clean install -Dmaven.test.skip=true</code></pre>
4. Locate the tar file in target directory
Path:
<pre><code>cd airavata/distribution/target/</code></pre>
5. Navigate to locally created directory (LocalAiravata) copy the tar file
<pre><code>cp airavata/distribution/target/apache-airavata-server-0.16-SNAPSHOT-bin.tar.gz ./</code></pre>
OR
<pre><code>cp airavata/distribution/target/apache-airavata-server-0.16-SNAPSHOT-bin.tar.zip ./</code></pre>
6. Now unzip either the tar or zip file of Airavata server distribution;
<pre><code>unzip apache-airavata-server-0.16-SNAPSHOT-bin.zip</code></pre>
OR
<pre><code>tar xvzf apache-airavata-server-0.16-SNAPSHOT-bin.tar.gz</code></pre>
7. Generate Credential store keystore file in the created local directory.
<pre><code>	keytool -genseckey -alias airavata -keyalg AES -keysize 128 -storetype jceks -keystore airavata_sym.jks</code></pre>
For more information visit <a href="https://cwiki.apache.org/confluence/display/AIRAVATA/Credential+Store+Configuration+Guide/" target="_blank">Credential Store Configuration Documentation</a>
8. In order to copy mysql.jar file; navigate to Airavata lib directory
<pre><code>cd /LocalFolderPath/apache-airavata-server-0.16-SNAPSHOT/lib</code></pre>
Now copy the mysql.jar to lib  directory (<a href="http://dev.mysql.com/downloads/connector/j/" target="_blank">Download mysql.jar</a>).
9. Navigate to bin folder which contains file airavata-server.properties and open it;
<pre><code>vi apache-airavata-server-0.16-SNAPSHOT/bin</code></pre>
10. Update relevant necessary properties in airavata-server.properties file.<br>
Change as required. For more details refer; <a href="../airavata-properties">Airavata Property File</a>.
	- In sections; API Server Registry Configuration, Application Catalog DB Configuration, Data Catalog DB Configuration, Workflow Catalog DB Configuration, Credential Store Module Configuration<br>
		- Comment out derby DB properties.<br>
		- Change MySQL configurations as per the databases created above.
	- Make sure gateway ID is properly defined;<br> 
		default.registry.gateway=php_reference_gateway
	- Server module Configuration
		- Make sure all servers required to start are added as given <br>
			servers=apiserver,orchestrator,gfac,credentialstore
	- API Server SSL Configurations
		- Give the correct path for key generation file. This is in the bin directory and it is shipped default with Airavata.<br>
		apiserver.keystore=/home/airavata/LocalAiravata/apache-airavata-server-0.16-SNAPSHOT/bin/airavata.jks
	- Credential Store module Configuration
		- Make sure its set to 'true' in<br>
		start.credential.store=true
		- Add the path to SSH key generation file <br>
		E.g.: credential.store.keystore.url=/home/airavata/LocalAiravata/airavata-sym.jks
	-  API Security Configuration
		- Make sure <br>
		api.secured=false<br>
		TLS.enabled=false
	-  Monitoring Module Configuration
      	- Add your email address, username and password for email monitoring.<br> This is the email account the job status change emails will be received from compute resources.
		 email.based.monitor.host=imap.gmail.com<br>
		 email.based.monitor.address=jobs@sample.org<br>
		 email.based.monitor.password=SamplePassword<br>
	-  Zookeeper Server Configuration
		- For 'Production' scenario make;<br>
		embedded.zk=false
	- AMQP Notification Configuration
		- Users can use RabbitMQ as 'Guest' users. This is the easy method. For this uncomment <br>
		rabbitmq.broker.url=amqp://localhost:5672
		- To use as a 'Production' user <br>
		Navigate to RabbitMQ bin folder.<br>
		Make sure the RabbitMQ server is running. For production use <pre><code>rabbitmq-server -detached</code></pre>
		Create a virtual-host and user with a password. Follow documentation in <a href="http://blog.dtzq.com/2012/06/rabbitmq-users-and-virtual-hosts.html" target="_blank">RabbitMQ Users & VirtualHost</a>
		To create a user; <pre><code>rabbitmqctl add_user airavata airavata</code></pre>
		To create a vitrual-host <pre><code>rabbitmqctl add_vhost messaging</code></pre>
		Provide permission to created username; 'airavata' to the created vhost <pre><code>rabbitmqctl set_permissions -p messaging airavata ".*" ".*" ".*”</code></pre>
		Uncomment rabbitmq.broker.url=amqp://airavata:airavata@localhost:5672/messaging.
11. Download and install Zookeeper. Use <a href="http://www.us.apache.org/dist/zookeeper/zookeeper-3.4.8/" target="_blank">Download Zookeeper</a> <br> You can download and install Zookeeper in the above created local folder; LocalAiravata
12. Start Zookeeper
    - Copy the sample config file to zoo.cfg:  cp conf/zoo_sample.cfg conf/zoo.cfg
    - Navigate to the Zookeeper bin directory and start zookeeper <pre><code>zkServer.sh start</code></pre>
13. In bin start the Airavata server and monitor log messages; This may require JAVA_HOME to be defined. Some configurations such as in  bin/zoo.cfg and bin/airavata-server.properties  may have to be adjusted if some ports are already in use. Ports need to be open as well.
<pre><code>sh airavata-server.sh start</code></pre> (This will run the airavata server in the background in demon mode)<br>
14. If you are in the target folder use given to start Airavata server;<br>
<pre><code>sh apache-airavata-server-0.16-SNAPSHOT/bin/airavata-server.sh start</code></pre>
15. To monitor the server starting up, view the airavata server log;<br>
<pre><code>tail -f airavata-server.out</code></pre>	
16. For subsequent Airavata copies; in the local Airavata folder where source code is cloned do a git clone https://github.com/apache/airavata.git for the latest trunk.