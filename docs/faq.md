## FAQs

<a href="#InstallFAQ">Installation FAQs</a></br>
<a href="#ConfigFGAQ">Configuration FAQs</a></br>
<a href="#userFAQ">User FAQs</a>

### <h3 id="InstallFAQ">Installation FAQs </h3>
<b class="blue"> Q1.</b> I have setup my own gateway and Airavata. When I log into the gateway I cannot create Compute resources. What should I do?</br>
<b class="blue">Answer: </b> In your pga_config.php (in folder .../testdrive/app/config) under heading 'Portal Related Configurations' set 'super-admin-portal' => false, to true.</br>

<br><b class="blue">Q2.</b> I don't get notifications when users create new accounts in my gateway. Why?</br>
<b class="blue">Answer: </b> That's because you have not defined an email address in <br>'admin-emails' => ['xxx@xxx.com','yyy@yyy.com']. Here you can add one or many.</br>

<br><br><b class="blue"> Q3.</b>  I am not receiving email notifications from compute resources for job status changes. What should I do?</br>
<b class="blue">Answer: </b> In airavata-server.properties please locate and set your email account information.
<pre><code>email.based.monitor.host=imap.gmail.com
email.based.monitor.address=airavata-user@kuytje.nl
email.based.monitor.password=zzzz
email.based.monitor.folder.name=INBOX
email.based.monitor.store.protocol=imaps (either imaps or pop3)</pre></code>
<br><br><b class="blue"> Q4.</b>  In my Airavata log I have error messages like
<br>ERROR org.apache.airavata.api.server.handler.AiravataServerHandler  - Error occurred while retrieving SSH public keys for gateway
<br>ERROR org.apache.airavata.credential.store.server.CredentialStoreServerHandler  - Error occurred while retrieving credentials
<br></br>What should I do?<br>
<br><b class="blue">Answer: </b> This could be due to missing tables in your credential store database. Check whether CREDENTIALS and COMMUNITY_USER tables exits. If not create then using
<pre><code>CREATE TABLE COMMUNITY_USER
(
        GATEWAY_ID VARCHAR(256) NOT NULL,
        COMMUNITY_USER_NAME VARCHAR(256) NOT NULL,
        TOKEN_ID VARCHAR(256) NOT NULL,
        COMMUNITY_USER_EMAIL VARCHAR(256) NOT NULL,
        PRIMARY KEY (GATEWAY_ID, COMMUNITY_USER_NAME, TOKEN_ID)
);
</pre></code>
<pre><code>CREATE TABLE CREDENTIALS
(
        GATEWAY_ID VARCHAR(256) NOT NULL,
        TOKEN_ID VARCHAR(256) NOT NULL,
        CREDENTIAL BLOB NOT NULL,
        PORTAL_USER_ID VARCHAR(256) NOT NULL,
        TIME_PERSISTED TIMESTAMP DEFAULT NOW() ON UPDATE NOW(),
        PRIMARY KEY (GATEWAY_ID, TOKEN_ID)
);
</pre></code>

<br><br><b class="blue"> Q5.</b>  I cannot login to my Compute Resource and launch jobs from Airavata using the SSH key I generated. What should I do?
<br><b class="blue">Answer: </b> Steps to use generated SSH key<br>
        - Generate SSH key + token using Credential Store<br>
        - Add the generated token to your resource through PGA --> Admin Dashboard --> Gateway Preferences<br>
        - Add the generated SSH key<br>

<br><b class="blue"> Q6.</b> When installing PGA in MAC i got below error after updating the composer.
    	<br>- Error<br>
    	Mcrypt PHP extension required.<br>
    	Script php artisan clear-compiled handling the post-update-cmd event returned with an error<br>
      		[RuntimeException]<br>
      		Error Output:
<br><b class="blue">Answer: </b>
      	Install mcrypt installation;
    	<a href="http://coolestguidesontheplanet.com/install-mcrypt-php-mac-osx-10-10-yosemite-development-server/" target="_blanks">mcrypt Installation Steps</a>

<br><b class="blue"> Q7.</b> After following the required steps only the home page is working and some images are not shown properly.
    <br><b class="blue">Answer: </b>If you are facing this behavior first check whether you have enabled mod_rewrite module in apache webserver.
    <br>And also check whether you have set AllowOverride All in the Vhost configuration file in apache web server. <br>(e.g file location is /etc/apache2/sites-available/default and there should be two places where you want to change)
<br><pre><code>
<VirtualHost *:80>
    ServerAdmin webmaster@dummy-host.example.com
    DocumentRoot /var/www/html/portal/public
    ServerName pga.example.com
    <Directory "/var/www/html/portal/public">
       AllowOverride all
    </Directory>
    ErrorLog logs/pga_error_log
    CustomLog logs/pga--access_log common
</VirtualHost></code></pre>
    <br>

<br><b class="blue"> Q8.</b> I get the Error message Permission Denied to app/storage directory.<br>
    <br><b class="blue">Answer: </b>Execute the following command and grant all permissions; <pre><code> sudo chmod -R 777 app/storage</code></pre>

<br><b class="blue"> Q9.</b> In Ubuntu environment when executing sudo composer update it fails with message "Mcrypt PHP extension required".
 <br><b class="blue">Answer: </b>To fix this install PHP mcrypt extension by following the below steps;
 <pre><code>sudo apt-get install php5-mcrypt</code></pre>
  Locate mcrypt.so ,to get its location
  Locate mcrypt.ini and open the mcrypt.ini file
    <pre><code>sudo pico /etc/php5/mods-available/mcrypt.ini</code></pre>
  Change the at line a extension=<location of the mcrypt.so file> eg:/usr/lib/php5/20121212/mcrypt.so Save changes.
  Execute the command:  <pre><code>sudo php5enmod mcrypt</code></pre>
  Now restart the apache server again and test PGA web-interface

<br><b class="blue"> Q10.</b> When tried to login or create a new user account an Error is thrown which is similar to PHP Fatal error:  SOAP-ERROR: Parsing WSDL: Couldn't load from...
    <br><b class="blue">Answer: </b> If you face this kind of an error first check whether you have enabled PHP SOAP and OpenSSL extensions. If even after enabling them the issue is still occurring try updating the PHP OpenSSL extension. (Using command like yum update openssl)
    
<br><b class="blue"> Q11.</b> If you are seeing an error similar to following in your airavata.log <br>
Error: ERROR org.apache.airavata.registry.core.app.catalog.impl.StorageResourceImpl  - Error while retrieving storage resource...
       javax.persistence.NoResultException: Query "SELECT p FROM StorageResource p WHERE p.storageResourceId =:param0" selected no result, but expected unique result.
<br><b class="blue">Answer: </b> Add storage resource ID in to the pga_config.php in your gateway code/app/config directory.  
         
<br><b class="blue"> Q12.</b> I am getting error <br>
2016-05-19 16:17:08,225 [main] ERROR org.apache.airavata.server.ServerMain  - Server Start Error:
java.lang.RuntimeException: Failed to create database connection pool. <br>

What should i do?
<br><b class="blue">Answer: </b> Airavata cannot create database connection because the mysql jar is not existing. Please follow step 8 of documentation in Installation --> Airavata --> Airavata Installation

### <h3 id="ConfigFGAQ">Configuration FAQs</h3>
<br><b class="blue"> Q1 </b> What each application input property mean? </br>
<b class="blue">Answer: </b> </br>
    - <b>Name:</b> </br>
    Identifier of the application input</br>
    - <b>Value:</b></br> 
    This could be a STRING value or it can also be used to set input file name.</br>
    - <b>Type: </b></br>
    Input type, List contain STRING, INTEGER, FLOAT, URI, STDOUT and STDERR</br>
    - <b>Application Arguments: </b></br>
    These are are the characters you would want on commandline in job execution for each input file or character input.</br>
    - <b>Standard Input: </b></br>
    Futuristic property and not in real use at the moment</br>
    -<b> User Friendly Description: </b></br>
    A description about the input to the gateway user. This will be displayed for users at experiment creation.</br>
    - <b>Input Order: </b></br>
    this is a number field. This will be the order inputs displayed in experiment creation.</br>
    - <b>Data is Staged:</b></br>
    - <b>Is the Input Required: </b></br>
    Futuristic property and not in real use at the moment. Whether set to true or false all inputs are currently treated as mandatory.</br>
    - <b>Required in Commandline:</b></br> 
    When this is set to true the arguments and the input file or the value will be available in job execution commandline in job script.</br>
    - <b>Meta Data:</b></br>

<br><b class="blue"> Q2 </b> Application Output Properties</br>
<b class="blue">Answer: </b>
<b>Add Application Output</b></br>
    - <b>Name:</b></br> 
    This is the label for the output.</br>
    - <b>Value:</b></br>
    This would be the actual name of the output airavata brings back to the PGA.</br>
    - <b>Type:</b></br>
    Tye of the output. This is mostly depended on the application. To troubleshoot for almost all applications define STDOUT and STDERR</br>
    - <b>Application Argument:</b></br>
    This would be arguments for outputs need to be in commandline.</br>
    - <b>Data Movement: </b></br>
    Futuristic property and not in real use at the moment. Whether set to true or false all outputs are currently brought back to PGA.</br>
    - <b>Is the Output required?:</b></br>
    - <b>Required on command line?:</b></br>
    When this is set to true the arguments and the output file or the value will be available in job execution commandline in job script.</br>
    - <b>Location:</b></br>
    - <b>Search Query:</b></br>	

<br><b class="blue"> Q3 </b> How to make input file available as an executable?</br>
<b class="blue">Answer: </b><br>
    - Input files defined are copied to the experiment working directory.</br>
    - Input files will be available in commandline when 'Required on Commandline' = true</br>
    - To add a commandline argument for a input file add 'Application Argument' for each input file. This will also define the order of files in commandline.</br>

<br><b class="blue"> Q4 </b> In Application Interface what is the use of 'Enable Optional File Inputs'	</br>
<b class="blue">Answer: </b></br>
    - By setting 'Enable Optional File Inputs' = true user can add none or many input files at experiment creation.</br>
    - In Airavata any input file required for the application to execute need to be defined as a separate input.</br>
    - When inputs are defined they are treated as 'Mandatory' inputs.</br>

<br><b class="blue"> Q5 </b> Where do I add remote resource execution commands?</br>
<b class="blue">Answer: </b>In Admin Dashboard --> Application Deployment </br>
- Add module load commands</br>
- Pre and post job commands</br>
- Environment variables

### <h3 id="userFAQ"> User FAQs </h3>
<b class="blue"> Q1 </b> What is the Project? </br>
<b class="blue">Answer: </b> </br>
    - Project is simply a collection of experiments. </br>
    - When creating an experiment it will be under the project you select.</br>
    - Projects can be shared with fellow gateway users. </br>
    - When the project is shared all experiments in the project will be shared as well.

<br><b class="blue"> Q2 </b> Where can I get test inputs? <br/>
<b class="blue">Answer: </b> If you need test inputs try downloading from <a href="https://iu.box.com/s/9ztdby709kso8siachz16svn2y511nn7" target="_blank">Test Input Files</a> <br/>

<br><b class="blue"> Q3 </b> Do I need to provide values for wall-time, node count and CPU count? OR can I go ahead with the given default values? <br/>
<b class="blue">Answer: </b> Default values are given to make life little easy for users. But depending on the job you should change the values. </br>E.g.: If you need only two or less cores than 16 better to change. If you need more wall-time change it, etc....<br/>
	
	
<br><b class="blue"> Q4 </b> What can I do with email Notifications in experiment? <br/>
<b class="blue">Answer: </b> Submitting a job from PGA does not guarantee job getting executed in the remote resource right away. If you add your email address, when the job starts and completes an email will be sent to you from the remote resource.<br/>

<br><b class="blue"> Q5 </b> Why 'Save' and 'Save and Launch'? <br>
<b class="blue">Answer: </b> User has the option of either create and 'Save' the experiment for later launch at remote resource <br/>Or <br/>
		can directly 'Save and Launch' at once.<br/>

<br><b class="blue"> Q6 </b> How do I monitor progress?<br/>
<b class="blue">Answer: </b> When the experiment is launched navigate to Experiment Summary Page.
		There the experiment and job status will be present.
		You can monitor the experiment and job status changes. Refresh the status using 'Refresh' icon on top  of the summary page.<br/>

<br><b class="blue"> Q7 </b> How do I view/download my outputs? <br/>
<b class="blue">Answer: </b> Same way you monitor the experiment progress! 
		<br/>For each experiment inputs can be downloaded from<br/>
		- Experiment Summary page<br/>
		- From 'Storage' at the top menu. Here you need to know the Project the experiment belongs to. 
		<br/> Once you locate the project you can browse for your experiment. <br/>

<br><b class="blue"> Q8 </b> I want to bring back all the outputs generated by my job. How?<br/>
<b class="blue">Answer: </b> You need to request your gateway admin to simply set Archive to 'true' in respective application interface in Admin Dashboard. Then all the files in the working directory will be brought back to PGA. This flag is set at gateway level not at individual user level.

<br><b class="blue"> Q9 </b> I want to cancel my experiment. How?<br/>
<b class="blue">Answer: </b> Navigate to experiment Summary and click 'Cancel' button.
	Experiments only in operation (LAUNCHED, EXECUTING experiment statuses) can be cancelled.

<br><b class="blue"> Q10 </b> 2. When I cancel do I still receive any outputs generated?<br/>
<b class="blue">Answer: </b> Files will be not transferred from the remote resource if the experiment is cancelled. However, if the output files were transferred to PGA data directories prior to the cancel request then they will be displayed.

<br><b class="blue"> Q11 </b> How can I run same application with different different inputs?<br/>
<b class="blue">Answer: </b> Simply clone an existing experiment and change the input files and launch.

<br><b class="blue"> Q12 </b> I want to change the wall-time of my experiment before launch. How can I do?<br/>
<b class="blue">Answer: </b> Experiments in CREATED state can be modified through Experiment Summary page. Click 'Edit' change values and Save or Save and Launch.
