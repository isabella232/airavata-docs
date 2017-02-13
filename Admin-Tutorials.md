## Admin Dashboard Configurations

This page is dedicated to Gateway Admins!

### Prior to starting your configurations make sure;
1. You have admin access to the PGA portal, Admin Dashboard
2. Storage resource ID added to the pga_config.php </br>
3. Credentials generated, updated in PGA and added to authorized_keys file in compute resources
4. Credentials generated, updated in PGA and added to authorized_keys file in storage resources

NOTE: If you are using a hosted gateway the 2 and 4 would be taken cared by the SciGaP team.

### Select Your Quick Start Tutorials
1. <a href="#LocalJob">Running Echo on Local Machine</a></br>
2. <a href="#GaussianJob">Gaussian Job Submission to Comet (XSEDE resource)</a></br>
3. <a href="#PrePostCommands">Add Environment Variables, Pre and Post Job Commands for an Application</a></br>
4. <a href="#SampleApp">Samples Application Configurations</a></br>
5. <a href= "#QOS&Reservation">Add Gateway QOS and Reservation for a Cluster</a></br>
6. <a href= "#Preference">Add Storage Resource Preferences</a></br>
<br>
</br>

#####<h5 id="LocalJob">Running Echo on Local Machine</h5>
Quickest way to confirm Airavata and PGA setup. This will tell you what you need to do to Echo a simple 'Hello World' in your local machine

1. Create new application module: Echo
    - Navigate to Admin Dashboard &rarr; App Catalog &rarr; Apllication Module 
    - Click Create a new Application Module
    - Enter Application Module Name: Echo
    - Enter Application Module Version: Echo 1.0 (Not mandatory)
    - Enter Description: Echo application for testing
    - Create
    - This create the Echo module </br>
![Screenshot](img/AppModule.png) </br></br>
2. Create the application interface: Echo
    - Navigate to Admin Dashboard &rarr; App Catalog &rarr; Application Interface
    - Click 'Create new Application Interface'
    - Add Application Name: Echo
    - Add Application Description: Echo Interface for testing
    - Select Application Module: Echo
    - Set 'Enable Archiving Working Directory' to False (Why? - This is set to true if you want to bring back all the files in working directory back to PGA)
    - Set 'Enable Optional File Inputs' to False (Why? - Set to false because there won't be any additional optional inputs for Echo)
    - Provide application inputs
        - Click Add Application Input
        - Name: Input-to-Echo
        - Value: Echo Test 1......2......3....... (This value can be overridden at experiment creation)
        - Type: STRING
        - Application Arguments:
        - Standard Input: False (Why? - Futuristic property and not in real use at the moment)
        - User Friendly Description: Enter STRING input for Echo (Not mandatory)
        - Input Order: 1
        - Data is Staged: True
        - Is the Input Required: True
        - Required in Commandline: True
        - Meta Data:
    - Provide application outputs
        - Click Add Application Output
        - Name: Echo-Standard-Out
        - Value:
        - Type: STDOUT
        - Application Argument:
        - Data Movement: False
        - Is the Output required?: True
        - Required on command line?: True
        - Location:
        - Search Query:</br>
![Screenshot](img/AppInterface1.png) ![Screenshot](img/AppInterface2.png) </br></br>
3. Create the application deployment: Echo on Local Machine
    - Navigate to Admin Dashboard &rarr; App Catalog &rarr; Application Deployment
    - Click 'Create new Application Deployment'
        - Application Module: Echo
        - Application Compute Host: Local (Local machine has to be added as a compute resource prior to this step)
        - Application Executable Path: /home/airavata/ECHO/echo_wrapper.sh (Local to where you have airavata installed)
        - Application Parallelism Type: SERIAL
4. Echo_wrapper.sh contains;
<pre><code>
    #!/bin/bash
    #sleep 4
    echo "Echoed_Output=$1" >> $2 2>> $3  
</code></pre>
           
#####<h5 id="GaussianJob">Gaussian Job Submission to Comet  (XSEDE resource)</h5>
This is a tutorial to configuring and running an application on XSEDE resource through PGA portal.
Work-in-Progress

Refer <a href="/Gateway-Configurations/#AppCatalog" target="_blank">Application Configuration</a> for more details.

