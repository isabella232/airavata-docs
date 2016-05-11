## Gateway Admin Maintenance Tasks

Gateway Admin's tasks could be mainly two types;

- Daily 
- Ad-hoc 
- Periodical or Planned 

### Daily Maintenance
###### Monitor Gateway Traffic
1. Investigate FAILED experiments or experiments which are requested to investigate by the users.
2. How to do this?
    - Navigate to AdminDashboard &#8658; Experiment Statistics
    - You could search for Experiments by giving the Creation Time 'To' and 'From'
    - Or using pre-defined selection criteria ('Get Experiments from Last 24 Hours' OR 'Get Experiments from Last Week') 
    
###### Disable Enable Compute Resources
1. Compute resources can be unreachable or with issues and not in a state for job submission.
2. In order to disable a resource
    - Navigate to AdminDashboard &#8658; Compute Resources &#8658; Browse
    - Un-check the  'Enabled' box for the specific resource
3. This will disable job submissions for the resource
