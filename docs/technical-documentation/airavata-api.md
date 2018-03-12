## Apache Airavata API

For Airavata API documentation please visit <a href="http://airavata.apache.org/api-docs/0.16/" target="_blank">Airavata 0.16 API Documentation</a>
### <h3>Airavata APIs for Experiments & Projects</h3>

|       Gateway Function/Feature        |           Airavata API            |           Description         |
|:--------------------------------------|:----------------------------------|:------------------------------|
<b style="color:blue;">Project</b>
| Create a Project                          | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_createProject" target="_blank">createProject</a>                                      | Linked with Create Project in PGA.    |
| Update Project                            | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_updateProject" target="_blank">updateProject</a>                                      | To update Project name and description.   |
| Get a Project                             | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getProject" target="_blank">getProject</a>                                            | Retrieve Project by providing the ID.           |
| Search Project by Name                    | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_searchProjectsByProjectName" target="_blank">searchProjectsByProjectName</a>          | Search for Project by giving part or full project name.          |
| Search Project by Desc                    | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_searchProjectsByProjectDesc" target="_blank">searchProjectsByProjectDesc</a>          | Search for Project by giving part or full project description.          |
| Get all user Projects                     | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getUserProjects" target="_blank">getUserProjects</a>                                  | Retrieve all Projects of a user.          |
<b style="color:blue;">Experiment</b>
| Create an Experiment                      | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_createExperiment" target="_blank">createExperiment</a>                                | Create an Experiment.          |
| Update an Experiment                      | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_updateExperiment" target="_blank">updateExperiment</a>                                | Update ab Experiment. Experiments with CREATED exp-status can be updated.          |
| Get an Experiment                         | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getExperiment" target="_blank">getExperiment</a>                                      | Retrieve Experiment by providing the experiment ID.          |
| Get Detailed Experiment                   | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getDetailedExperimentTree" target="_blank">getDetailedExperimentTree</a>              | Retrieve detailed Experiment by providing the experiment ID.          |
| Clone an Experiment                       | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_cloneExperiment" target="_blank">cloneExperiment</a>                                  | Clone an existing Experiment. Experiment with any exp-status can be cloned by providing the ID.          |
| Cancel an Experiment                      | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_terminateExperiment" target="_blank">terminateExperiment</a>                          | Cancel an existing Experiment. Experiments with exp-statuses LAUNCHING or EXECUTING can be cancelled.           |
| Search Experiment by Name                 | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_searchExperimentsByName" target="_blank">searchExperimentsByName</a>                  | Search Experiment by giving full or part of the name.          |
| Search Experiment by Desc                 | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_searchExperimentsByDesc" target="_blank">searchExperimentsByDesc</a>                  | Search Experiment by giving full or part of the description.           |
| Search Experiments by Application Name    | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_searchExperimentsByApplication" target="_blank">searchExperimentsByApplication</a>    | Search Experiment by giving the application name.           |
| Search Experiment by Creation Time        | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_searchExperimentsByCreationTime" target="_blank">searchExperimentsByCreationTime</a>  | Search Experiment by giving creationTime period.           |
| Get all user Experiments                  | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getUserExperiments" target="_blank">getUserExperiments</a>                            | Search for all the experiments of a single user.          |
| Get Experiments for a Project             | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getExperimentsInProject" target="_blank">getExperimentsInProject</a>                  | Retrieve all the experiments in a particular Project.          |





### <h3>Airavata APIs for Admin Dashboard</h3>
   
|           Admin Function/Feature              |              Airavata API             |                                          Description                                              |
|:----------------------------------------------|:--------------------------------------|:------------------------------------------------------------------------------------------------  |
<b style="color:blue;">Add Gateway</b>
| Add a gateway                                 | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_addGateway" target="_blank">addGateway</a>        | Adding a new Gateway. |
<b style="color:blue;">Credential Store</b>  
| Generate a Token/SSH Key                      | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_generateAndRegisterSSHKeys" target="_blank">generateAndRegisterSSHKeys</a>            | Generate new SSH Key and Token.   |
| Get all Credential Store Tokens               | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getAllGatewaySSHPubKeys" target="_blank">getAllGatewaySSHPubKeys</a>               | Retrieve all the generated keys of a Gateway.              |
| Remove a Token/SSH Key                        | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_deleteSSHPubKey" target="_blank">deleteSSHPubKey</a>                       | Select and delete a particular SSH Key Token pair.   |  
<b style="color:blue;">Compute Resource (CR)</b>                                                                                            
| Get all application deployed CRs              | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getAllApplicationDeployments" target="_blank">getAllApplicationDeployments</a>          | Get all Application deployed Compute Resources.        |
| Get a CR                                      | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getComputeResource" target="_blank">getComputeResource</a>                    | Retrieve Compute Resource information by providing the resource ID.   |
| Register CR                                   | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_registerComputeResource" target="_blank">registerComputeResource</a>               | Register a new Compute Resource. This is Super Admin Feature.|
| Update CR                                     | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_updateComputeResource" target="_blank">updateComputeResource</a>                 | Retrieve an existing Compute Resource and update.|
| Enable and Disable CR                         | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getComputeResource" target="_blank">getComputeResource</a>    <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_updateComputeResource" target="_blank">updateComputeResource</a>    | Retrieve the CR and enable or disable through update. This is a Super Admin feature.| 
| Delete a Queue                                | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_deleteBatchQueue" target="_blank">deleteBatchQueue</a>                      | Delete a selected Queue from the Compute Resource.      |
<b style="color:blue;">Storage Resource (SR)</b> 
| Get all SR Names                              | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getAllStorageResourceNames" target="_blank">getAllStorageResourceNames</a>          | Retrieve all storage resources of the gateway.  |
| Get a SR                                      | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getStorageResource" target="_blank">getStorageResource</a>                    | Fetch Storage Resource by providing the Storage ID.   | 
| Register a SR                                 | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_registerStorageResource" target="_blank">registerStorageResource</a>               | Register a new Storage Resource. This is a Super Admin Feature.|
| Update a SR                                   | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_updateStorageResource" target="_blank">updateStorageResource</a>                 | Update and existing Storage Resource.|
| Enable and Disable SR                         | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getStorageResource" target="_blank">getStorageResource</a>    <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_updateStorageResource" target="_blank">updateStorageResource</a>    |Retrieve the SR and enable or disable through update. This is a Super Admin feature.|
| Delete SR                                     | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_deleteStorageResource" target="_blank">deleteStorageResource</a>                 |Select and delete and existing Storage Resource. |
| Delete Data Movement Interface of SR          | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_deleteDataMovementInterface" target="_blank">deleteDataMovementInterface</a>       |Delete a Data Movement Interface of a Storage Resource|
<b style="color:blue;">Experiment Statistics</b>
| Get Experiment Statistics                     | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_getExperimentStatistics" target="_blank">getExperimentStatistics</a>               | Displays experiments grouped by the experiment status and derived for the given date time range.  |
<b style="color:blue;">Gateway Preferences</b>
| Add CR Preference for a gateway               | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_addGatewayComputeResourcePreference" target="_blank"> addGatewayComputeResourcePreference</a>     ||     
| Edit CR Preference                            | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_addGatewayComputeResourcePreference" target="_blank"> addGatewayComputeResourcePreference</a>     ||
| Delete a CR Preference                        |  ||
| Add SR Preference for a gateway               | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_addGatewayStoragePreference" target="_blank"> addGatewayStoragePreference</a>     || 
| Edit SR Preference                            | <a href="http://airavata.apache.org/api-docs/0.16/airavata_api.html#Fn_Airavata_addGatewayStoragePreference" target="_blank"> addGatewayStoragePreference</a>     ||
| Delete a SR Preference                        |      ||
<b style="color:blue;">Other</b>
| Get all Notices                               | noticesView                           | View all existing Notices.        |





<br></br>
If any questions or clarification regarding the API documentation please contact us through;
<a href="http://airavata.apache.org/community/mailing-lists.html" target="_blank"><br>Airavata Mailing List</a> <br> OR<br>
<a href="https://www.hipchat.com/gMDHyN1KM" target="_blank">HipChat</a>
