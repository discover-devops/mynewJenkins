Setting up a Jenkins slave node with passwordless SSH involves a few steps. 
Below is a step-by-step guide to help you achieve this:

### Prerequisites:
1. Jenkins Master Server: Ensure that Jenkins is installed on the master server.
2. Jenkins Slave Server: Set up a server that will act as the Jenkins slave.
3. SSH Installed: Make sure that SSH is installed on both the master and slave servers.
4. Jenkins Plugins: Install the "SSH Agent" and "SSH Slaves" plugins on the Jenkins master.

### Step 1: Generate SSH Key Pair on Master Server
1. Open a terminal on the Jenkins master server.
2. Run the following command to generate an SSH key pair:

    ```bash
    ssh-keygen -t rsa
    ```

   Press Enter to accept the default file locations.

### Step 2: Copy SSH Public Key to Jenkins Slave
1. Use the following command to copy the public key to the Jenkins slave server:

    ```bash
    ssh-copy-id username@jenkins-slave-server
    ```

   Replace `username` with your actual username and `jenkins-slave-server` with the IP address or hostname of your Jenkins slave server.

### Step 3: Configure Jenkins Master
1. Open Jenkins in your web browser.
2. Navigate to "Manage Jenkins" > "Manage Nodes and Clouds."
3. Click on "New Node" to create a new slave node.
4. Enter a node name and choose "Permanent Agent."
5. Configure the following:
   - **# of Executors:** Number of concurrent builds the node can handle.
   - **Remote Directory:** The directory where Jenkins will perform builds.
   - **Labels:** Optional labels to restrict jobs to specific nodes.
   - **Launch Method:** Select "Launch agent agents via SSH."
   - **Host:** Jenkins slave server IP or hostname.
   - **Credentials:** Click on "Add" to add SSH credentials.
   
     Provide your username, private key, and passphrase if used.


![image](https://github.com/discover-devops/mynewJenkins/assets/53135263/0fa55348-4101-4a19-8165-d2e441a868b8)






6. Click "Save" to save the configuration.

### Step 4: Verify Connection
1. Go back to the "Manage Nodes and Clouds" page in Jenkins.
2. You should see your newly added node listed. Click on the node name.
3. Click on "Launch agent" to verify the connection.

### Step 5: Test a Jenkins Job
1. Create or use an existing Jenkins job.
2. In the job configuration, specify the label you set in Step 3 (if any) to ensure it runs on the slave node.
3. Build the job and verify that it runs on the Jenkins slave.

Now, your Jenkins master should be able to communicate with the slave node using passwordless SSH. Adjust the instructions based on your specific setup and requirements.
