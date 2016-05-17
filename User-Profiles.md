## Apache Airavata User Profiles

### What Are Airavata User Roles?

1. Prior to using Airavata as the middleware between your gateway and computational resources, lets identify and understand the user roles available and their access levels.
2. Knowing the roles and the features of each will assist on shaping your gateway user hierarchy.
3. There are 4 active user roles in Airavata with different set of features at each level.
	- Admin
	- Admin-Read-Only
	- Gateway-User
	- User-Pending

### What each User Role can do within PGA?

1. Admin User
	- Set up gateway preferences for Compute Resources and Storage Resources
	- Generate SSH keys and their tokens using Credential Store in Admin Dashboard.
	- Add the generated SSH token to Gateway Preferences.
	- Add the generated SSH keys to authorized_key files in each resource.
	- Can Cancel, clone experiments of a gateway user through Admin dashboard behalf of the user.
	- Create Applications and their deployments in to the gateway.
<br><b>NOTE: If user hosts his own gateway; 'Gateway Admin' role will hold features of both Super Admin and Gateway Admin.</b></br><br>

2. Admin-Read-Only
	- Can view everything in Admin Dashboard but cannot Add, Edit or Delete any records from dashboard.
	- Can monitor experiments through Experiments Statistics in Admin dashboard.
	- Behalf of a gateway user can edit, cancel or clone an experiment.
<br></br>
3. General User
	- Create, launch their own experiments in using available applications and compute resources.
	- Monitor progress of experiment execution.
	- Group experiments by creating Projects.
	- Request new features, applications and report bug, issue using Service Desk
	- Password recovery.
<br>
</br>
4. User-Pending
	- This is the initial role assigned to users when account is created.
	- Until gateway admin assigns a different role user has no real access to the gateway with this role.
<br>
</br>
### How User Roles Work?

1. Users can have one or many user roles assigned to them.
2. Every time a role changes user will be notified through email about the privilege change.