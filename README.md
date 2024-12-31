# cicd-project (todo application)


Create an EC2 instance with Ubuntu as OS image

Install Jenkins on ec2 instance using following commands:

`sudo apt update `


`sudo apt install openjdk-17-jre`

Check if java is installed (most important)

`java -version `

`curl -fsSL https://pkg.jenkins.io/debian/jenkins.io-2023.key | sudo tee   /usr/share/keyrings/jenkins-keyring.asc > /dev/null`

`echo deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]   https://pkg.jenkins.io/debian binary/ | sudo tee   /etc/apt/sources.list.d/jenkins.list > /dev/null`

`sudo apt-get update `

`sudo apt-get install Jenkins`

Allow HTTP traffic on port 8080

Use your public Private IP of ec2 instance followed by port 8080 to run Jenkins on browser

Fetch the password for login to Jenkins:
`sudo cat /var/lib/jenkins/secrets/initialAdminPassword`

Create new item in Jenkins

Add git repo

Set to puclic if repo is public

If repo is private do `ssh-keygen` on linux terminal, generate id_rsa(private) and id_rsa.pub(public).

Paste the id_rsa.pub(public) in ssh keys of github account. This will connect github with Jenkins

Do build now , This will create the app directory in Jenkins.

Install Docker on ec2 instance:
`sudo apt install docker.io`

Create a Dockerfile

Give permissions to add ubuntu user to docker server:
`sudo usermod -a -G docker $USER`
`sudo reboot`

Build a docker container for the application:
`docker build . -t todo-app `

Run the docker container:
`docker run -d --name node-todo-app -p 8000:8000 todo-app`

For automating the running of docker container through Jenkins pipeline:
Go to Jenkins Job -> configure -> Add build steps -> Execute shell -> Add docker build and run commands

If while building pipeline there is error of permission denied by docker deamon then execute following in linux machine:
`Sudo usermod -a -G docker Jenkins`
`Sudo systemctl restart Jenkins`

Now build the pipeline and Jenkins will execute docker commands

Now for running application as soon as code is pushed in github repo , install "github-integration" plugin in Jenkins

Connect github with Jenkins using ssh key

Add a webhook in github where the payload url will be Jenkins url

This will trigger the Jenkins pipeline as soon as code is pushed in github repo

