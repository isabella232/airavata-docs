## Apache Airavata API

For Airavata API documentation please visit <a href="http://airavata.apache.org/api-docs/0.16/" target="_blank">Airavata 0.16 API Documentation</a>
### <h3>Airavata APIs for Experiments & Projects</h3>
###### <h6 style="color:#922B21;">Project</h6>

|       Gateway Function/Feature        |           Airavata API            |           Description         |
|:--------------------------------------|:----------------------------------|:------------------------------|
<b style="color:blue;">Project</b>
| Create a Project                      | createProject                     |           |
| Update Project                        | updateProject                     |           |
| Get a Project                         | getProject                        |           |
| Search Project by Name                | searchProjectsByProjectName       |           |
| Search Project by Desc                | searchProjectsByProjectDesc       |           |
| Get all user Projects                 | getUserProjects                   |           |
<b style="color:blue;">Experiment</b>
| Create an Experiment                  | createExperiment                     |           |
| Update an Experiment                         | updateExperiment                     |           |
| Get an Experiment                         | getExperiment                        |           |
| Get Detailed Experiment                   | getDetailedExperimentTree             |           |
| Clone an Experiment                      | cloneExperiment                   |                |
| Cancel an Experiment                     | terminateExperiment               |            |
| Search Experiment by Name                | searchExperimentsByName       |           |
| Search Experiment by Desc                | searchExperimentsByDesc       |           |
| Search Experiments by Application Name    | searchExperimentsByApplication    |           |
| Search Experiment by Creation Time        | searchExperimentsByCreationTime
| Get all user Experiments                 | getUserProjects                   |           |
| Get Experiments for a Project            | getExperimentsInProject           |           |





### <h3>Airavata APIs for Admin Dashboard</h3>
###### <h6 style="color:#922B21;">Experiment Statistics</h6>
   
|           Admin Function/Feature              |              Airavata API             |                                          Description                                              |
|:----------------------------------------------|:--------------------------------------|:------------------------------------------------------------------------------------------------  |
<b style="color:blue;">Add Gateway</b>
| Add a gateway | addGateway        |
<b style="color:blue;">Credential Store</b>  
| Generate a Token/SSH Key                      | generateAndRegisterSSHKeys            |   |
| Get all Credential Store Tokens               | getAllGatewaySSHPubKeys               |                                                                                                   |
| Remove a Token/SSH Key                        | deleteSSHPubKey                       |   |  
| Get all Notices                               | noticesView                           |                      |
<b style="color:blue;">Compute Resource (CR)</b>                                                                                            
| Get all CRs                     | getAllApplicationDeployments          |                                                                                                   |
| Get a CR                       | getStorageResource                    |
| Register CR                     | registerComputeResource               |
| Update CR                       | updateComputeResource                 ||
| Enable and Disable CR          | getComputeResource    updateComputeResource    |
<b style="color:blue;">Storage Resource (SR)</b> 
| Get all SRs                                   | getAllApplicationDeployments          |                                                                                                   |
| Get a SR                                      | getComputeResource                    |
| Register a SR                     | registerStorageResource               |
| Update a SR                      | updateStorageResource                 ||
| Enable and Disable SR           | getStorageResource    updateStorageResource    |
| Delete SR                       | deleteStorageResource                 |
| Delete Data Movement Interface of SR  | deleteDataMovementInterface       |
<b style="color:blue;">Experiment Statistics</b>
| Get Experiment Statistics                     | getExperimentStatistics               | Displays experiments grouped by the experiment status and derived for the given date time range.  |






<br></br>
If any questions or clarification regarding the API documentation please contact us through;
<a href="http://airavata.apache.org/community/mailing-lists.html" target="_blank"><br>Airavata Mailing List</a> <br> OR<br>
<a href="https://www.hipchat.com/gMDHyN1KM" target="_blank">HipChat</a>
