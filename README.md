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


Run these commands:


`sudo apt install nodejs`


`sudo apt install npm`


`npm install`

`node app.js`

or Run by docker compose

test

