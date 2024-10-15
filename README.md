# Jenkins-project
Installing Jenkins on the EC2 instance and running the jobs using the Docker agent to make it more efficient and less cost reliant

## Installation on EC2 Instance ##

### Go to AWS Console ###
Instances(running)
Launch instances

### Install Jenkins ###

`sudo apt update`

`sudo apt install openjdk-17-jre`

### Verify the installation ###

`java --version`

### Curl and install jenkins ###

`curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee \
  /usr/share/keyrings/jenkins-keyring.asc > /dev/null`
  
`echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc] \
  https://pkg.jenkins.io/debian binary/ | sudo tee \
  /etc/apt/sources.list.d/jenkins.list > /dev/null`

`sudo apt-get update`

`sudo apt-get install jenkins`

By default, Jenkins will not be accessible to the external world due to the inbound traffic restriction by AWS. Open port 8080 in the inbound traffic rules as show below.

EC2 > Instances > Click on
In the bottom tabs -> Click on Security
Security groups
Add inbound traffic rules as shown in the image (you can just allow TCP 8080 as well, in my case, I allowed All traffic).

### Login to Jenkins using the below URL: ###

publicIP:8080

After logging in , install the Suggested plugins

### Install the Docker Pipeline plugin in Jenkins: ###

Log in to Jenkins.
Go to Manage Jenkins > Manage Plugins.
In the Available tab, search for "Docker Pipeline".
Select the plugin and click the Install button.
Restart Jenkins after the plugin is installed.

### Configure Docker before you follow the steps above , ###

`sudo apt install docker.io`

### Grant jenkin access to docker to execute the pipeline ###

`sudo su - `

`usermod -aG docker jenkins`

`systemctl restart docker`

### Once you are done with the above steps, it is better to restart Jenkins. ###

`http://<ec2-instance-public-ip>:8080/restart`

## Run your first Job ##

There are many other options to run the jobs , one of the few methods mostly used are Freestyle and Pipeline

We will go with Pipeline and select the Source Code Management (SCM) as this Github repo and click on **click Build Now to run the job.**

Once the job starts, you can monitor its progress in the **Build History section.**
