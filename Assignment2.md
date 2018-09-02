#  **Assignment 2 - Jenkins**
## Installing Blue Ocean
* Go to Manage Jenkins > Manage Plugins.
* Choose the Available tab and search for blue ocean.
* Select the Blue Ocean (BlueOcean Aggregator) plugin. The docs recommend installing only this one since all other * Blue Ocean plugins will be installed automatically (as dependencies).
* Blue Ocean will be activated when Jenkins restarts.
* Choose the Blue Ocean option from the left menu to use the Blue Ocean UI.

## Building Private Github Repository
* Create a new freestyle project
* Select Git in the section Source Code Management
* In the input field Repository URL enter the URL of your private repository.
* Since the repository is private, jenkins will not be able to access it without credentials. Click on Add in the Credentials input field and enter your github credentials.
* Once added, select the credentials from the dropdown menu for Credentials.
* You can select the branches to build or leave it as */master (default).
*Now the private repository can be used like any other public repository.

## Using Git SCM Poll
( You will need to map your localhost:8080 (where jenkins is running) to a public IP for this.

* Go to Build Triggers section and choose GitHub hook trigger for GITScm polling.

* **Getting a Public IP (using ngrok)**
1. You can get the public IP of your localhost:8080 (where jenkins is running) using ngrok.
2. Go to ngrok's official site and follow the instructions to install ngrok.
3. Run ./ngrok http 8080 (to map 8080 which is the jenkins port to a public IP). You will get a public IP of the form http://<SOMETHING>.ngrok.io, use this in the webhook.
* **Setting up webhook in the Github repository.**
1. Navigate to Settings in your Github repository.
2. Go to Webhooks -> Add webhook.
3. Enter http://<public-ip or URL>/github-webhook/ in Payload URL.
4. Select Content type as application/json.
5. You can select Which events would you like to trigger this webhook? as per requirements.
6. The Active option should be selected.
7. Now Github will make a request to the Jenkins webhook and cause a build whenever required.

## Post-build Actions - Archive the artifacts
Here, we adding the Archive post build action. This will archive selected files.

* Select the project and go to Configure > Post-build Actions
* Click the Add post-build action button and select Archive the artifacts
* Select the files that you want to archive (eg: * will archive all the files)
* Click the Advanced button
* Select
1. Use default excludes
2. Archive artifacts only if build is successful
* This will archive all files in the linked github repo when the build is successful