## WSO2 Identity Server (IS) Installation

### Installation
1. Download IS 5.1.0 from <a href="http://wso2.com/products/identity-server/" target="_blank">WSO2 Site</a> and extract it.
2. Open &#60;IS_HOME&#62;/repository/conf/carbon.xml and set the HideAdminServiceWSDLs property to false.
<pre><code>&#60;HideAdminServiceWSDLs&#62;false&#60;/HideAdminServiceWSDLs&#62;</code></pre>
3. To enable self signup and account confirmation follow the below steps
    - Open &#60;IS_HOME&#62;/repository/conf/claim-config.xml and add the following claims mappings in the &#60;Dialect dialectURI="http://wso2.org/claims"&#62; section.
<pre><code>&#60;Claim&#62;
          &#60;ClaimURI&#62;http://wso2.org/claims/identity/accountLocked&#60;/ClaimURI&#62;
          &#60;DisplayName&#62;Account Locked&#60;/DisplayName&#62;
          &#60;AttributeID&#62;accountLock&#60;/AttributeID&#62;
          &#60;Description&#62;Account Locked&#60;/Description&#62;
&#60;/Claim&#62;
&#60;Claim&#62;
          &#60;ClaimURI&#62;http://wso2.org/claims/identity/passwordTimestamp&#60;/ClaimURI&#62;
          &#60;DisplayName&#62;Password Timestamp&#60;/DisplayName&#62;
          &#60;AttributeID&#62;facsimileTelephoneNumber&#60;/AttributeID&#62;
          &#60;Description&#62;Password Timestamp&#60;/Description&#62;
&#60;/Claim&#62;
&#60;Claim&#62;
          &#60;ClaimURI&#62;http://wso2.org/claims/username&#60;/ClaimURI&#62;
          &#60;DisplayName&#62;Username&#60;/DisplayName&#62;
          &#60;AttributeID&#62;uid&#60;/AttributeID&#62;
          &#60;Description&#62;Username&#60;/Description&#62;
&#60;/Claim&#62;
</code></pre>
    - Open &#60;IS_HOME&#62;/repository/conf/claim-config.xml and add the following claims mappings in the &#60;Dialect dialectURI="http://wso2.org/oidc/claim"&#62; section.
<pre><code>&#60;Claim&#62;
          &#60;ClaimURI&#62;roles&#60;/ClaimURI&#62;
          &#60;DisplayName&#62;Roles&#60;/DisplayName&#62;
          &#60;AttributeID&#62;role&#60;/AttributeID&#62;
          &#60;Description&#62;Roles&#60;/Description&#62;
&#60;/Claim&#62;
</code></pre>
<br>

    - Enable the Identity Listener by setting the following property to true in the &#60;IS_HOME&#62;/repository/conf/identity/identity.xml file.
<pre><code>&#60;EventListener type="org.wso2.carbon.user.core.listener.UserOperationEventListener" name="org.wso2.carbon.identity.mgt.IdentityMgtEventListener" orderId="50" enable="true"/&#62;</code></pre>

    - Do the following configurations in the &#60;IS_HOME&#62;/repository/conf/identity/identity­-mgt.properties file.
<pre><code>
Notification.Sending.Internally.Managed=true
Authentication.Policy.Account.Lock.On.Creation=true
Notification.Expire.Time=7200
Notification.Sending.Enable=true
Authentication.Policy.Enable=true
</code></pre>

    - Configure the email-admin-config.xml file found in &#60;IS_HOME&#62;/repository/conf/email/ with the email template of type “accountConfirmation”.

    - Edit the org.apache.axis2.transport.mail.MailTransportSender section in the &#60;IS_HOME&#62;/repository/conf/axis2/axis2.xml to valid email account configuration. 
<br>IS server should have access to this email account for remotely login.
<pre><code>
&#60;transportSender name="mailto"class="org.apache.axis2.transport.mail.MailTransportSender"&#62;
        &#60;parameter name="mail.smtp.from"&#62;wso2demomail@gmail.com&#60;/parameter&#62;
        &#60;parameter name="mail.smtp.user"&#62;wso2demomail&#60;/parameter&#62;
        &#60;parameter name="mail.smtp.password"&#62;mailpassword&#60;/parameter&#62;
        &#60;parameter name="mail.smtp.host"&#62;smtp.gmail.com&#60;/parameter&#62;
        &#60;parameter name="mail.smtp.port"&#62;587&#60;/parameter&#62;
        &#60;parameter name="mail.smtp.starttls.enable"&#62;true&#60;/parameter&#62;
        &#60;parameter name="mail.smtp.auth"&#62;true&#60;/parameter&#62;
&#60;/transportSender&#62;
</code></pre>

4. Go to &#60;IS_HOME&#62;/bin and start IS server using ./wso2server.sh (use ./wso2server.sh start for starting in daemon mode).

### WSO2 IS Configuration
1. Creating a new tenant.
2. Registering a new OAuth Service Provider.

### Optional Steps
1. How to configure a mysql backend database for wso2 IS server - <a href="https://docs.wso2.com/display/IS510/Setting+up+MySQL" target="_blank">MySQL DB Configuration</a>
2. How to configure a valid server certificate for the wso2 IS server - <a href="http://wso2.com/library/knowledge-base/2011/08/adding-ca-certificate-authority-signed-certificate-wso2-products/" target="_blank">Configure Server Certificate</a>
