## Gateway Maintenance

<br><b class="blue">Q1.</b> One of my gateway users wants me to investigate his FAILED experiment. How should I proceed?
<br><b class="blue">Answer:</b> To investigate a specific FAILED experiment or failed experiment within a time frame,<br>
1. Navigate to AdminDashboard &#8658; Experiment Statistics <br>
2. Search the experiment by using the experiment ID or by giving the Creation Time 'To' and 'From' <br>
3. You could also use pre-defined selection criteria ('Get Experiments from Last 24 Hours' OR 'Get Experiments from Last Week') <br>

<br><b class="blue">Q2.</b> One of the resources used by my gateway is not available for the day. How to stop user job submissions?
<br><b class="blue">Answer:</b> To temporarily stop users submitting jobs to a particular resource...<br>
1. Navigate to AdminDashboard &#8658; Compute Resources (Browse)<br>
2. Un-check the  'Enabled' box for the specific resource. This disables job submissions for the resource<br>
3. To enable job submission simply check the box and back in track!<br>

<br><b class="blue">Q3.</b> How to upgrade access for a gateway user?
<br><b class="blue">Answer:</b> User access can be upgraded or downgraded by changing the assigned user role.<br>
1. Navigate to Admin Dashboard &#8658; Users (Browse)<br>
2. Search for the specific user and click 'Check All Roles'<br>
3. From this you can remove/add roles.<br>
4. For each modification user will receive an email with 'Your Privileges has Changed!'<br>

<br><b class="blue">Q4.</b> Gateway users who has role 'gateway-user' cannot access experiment creation. Seems like privileges are not accessible.!
<br><b class="blue">Answer:</b> User roles are given through PGA Admin Dashboard. If the roles are set correctly then check pga_config.php<br>
1. To check the config file use
<pre><code>vi /var/www/html/airavata-php-gateway/app/config/pga_config.php</code></pre>
2. Roles attached to users should exists in the config file against correct role attribute type
<pre><code>
        /**
         * Admin Role Name
         */
        'admin-role-name' => 'admin',
        /**
         * Read only Admin Role Name
         */
        'read-only-admin-role-name' => 'admin-read-only',
        /**
         * Gateway user role
         */
        'user-role-name' => 'airavata-user',
</code></pre>

<br><b class="blue">Q5.</b> I have ran out of allocation for my current community account used in gateway for a resource. What should I do?
<br><b class="blue">Answer:</b><br> 
1. If you have another community account you could update the information in Admin Dashboard &#8658; Gateway Profile under Compute Resource Preferences.<br>
2. Select the resource and modify account information and save.<br>
3. Login to the resource as the new user and update the authorized_keys with the public key assigned to the resource.<br>


