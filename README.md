# jenkins
Jenkins Installation Steps:-
Update Packages:
sudo apt-get update

Install Java:
sudo apt install openjdk-11-jdk -y

Add Repositories:
sudo wget -O /usr/share/keyrings/jenkins-keyring.asc   https://pkg.jenkins.io/debian-stable/jenkins.io-2023.key
echo "deb [signed-by=/usr/share/keyrings/jenkins-keyring.asc]"   https://pkg.jenkins.io/debian-stable binary/ | sudo tee   /etc/apt/sources.list.d/jenkins.list > /dev/null

Update Packages:
sudo apt-get update

Install Jenkins:
sudo apt-get install jenkins

Start & Enable Jenkins:
sudo systemctl start jenkins
sudo systemctl enable jenkins
sudo systemctl status jenkins

Install Java on Slave Node:
sudo apt install openjdk-11-jdk -y


Configure node in Jenkins and execute the Jar on the Slave Node.

Also Go to Manage Jenkins --> Security --> TCP port for inbound agents
Either Select Fixed or Random. If it's disabled, agents won't be able to connect.