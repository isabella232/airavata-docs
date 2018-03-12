## Apache Airavata Update

1. In order to update Airavata with latest master code; go to the folder (Created in installation; LocalAiravata) initially created to clone Airavata.
2. Within your local folder navigate to folder 'airavata' and execute <pre><code>git pull </code></pre>
Hint: If you are in the wrong folder you would probably get message <pre><code>'fatal: Not a git repository (or any of the parent directories): .git'</code></pre>
3. Now build the code 
<pre><code> mvn clean install</code></pre>
Hint: To avoid the 'tests on install' run <pre><code>mvn clean install -Dmaven.test.skip=true</code></pre>
4. Once the build is success, stop the running Airavata server. You can either stop the java server using 
<pre><code>kill -9 &#60;process ID&#62;</code></pre>
OR<br>
Navigate to bin folder where airavata server exists (LocalAiravata/apache-airavata-server-0.15-SNAPSHOT/bin). and stop the server
<pre><code>./airavata-server.sh stop -force</code></pre>
5. For references, back up the currently existing release
<pre><code>mv apache-airavata-server-0.15-SNAPSHOT apache-airavata-server-0.15-SNAPSHOT-bk</code></pre>
6. Copy the new release to your local folder (LocalAiravata)
<pre><code>cp /&#60;path to created folder&#62;/LocalAiravata/airavata/distribution/target/apache-airavata-server-0.16-SNAPSHOT-bin.tar.gz .</code></pre>
7. Un-tar the copied new release
<pre><code>tar -xvf apache-airavata-server-0.16-SNAPSHOT-bin.tar.gz</code></pre>
8. Navigate to the new bin folder and back up airavata-server.properties and gfac-config.yaml files.
9. Copy your previously used airavata-server.properties from the backed up release to bin folder (This is the easiest way to get the properties file updated. If you prefer, you can change the new file manually. &#9786;)
<pre><code>/&#60;your local path&#62;/LocalAiravata/LocalAiravata/apache-airavata-server-0.16-SNAPSHOT-bk/bin/airavata-server.properties .</code></pre>
10. Copy your previously used gfac-config.yaml from the backed up release
<pre><code>cp /&#60;your local path&#62;/LocalAiravata/apache-airavata-server-0.16-SNAPSHOT-bk/bin/gfac-config.yaml .</code></pre>
11. Now compare with the new airavata-server.properties and gfac-config.yaml and make necessary changes in the copied files.
Try <pre><code> diff airavata-server.properties airavata-server.properties-bk</code></pre>
12. Check the path correctness of credential store keystore in airavata-server.properties file.
<pre><code>credential.store.keystore.url=/&#60;your local path&#62;/LocalAiravata/airavata_sym.jks</code></pre>
13. Go to lib folder and copy mySQL jar (mysql-connector-java-5.1.38-bin.jar) from old backed up lib to the new lib
<pre><code>  cp /home/airavata/LocalAiravata/apache-airavata-server-0.16-SNAPSHOT-bk/lib/mysql-connector-java-5.1.38-bin.jar .</code></pre>
14. Now restart airavata server in bin folder
<pre><code>./airavata-server.sh start</code></pre>
15. Airavata ready for job submissions!
16. For PGA updating steps try [PGA Update](pga-update.md).
