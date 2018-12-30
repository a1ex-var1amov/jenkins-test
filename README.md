# jenkins-test
## Jenkins config

***1.Jenkins and pylint installation***
```
yum install java-1.8.0-openjdk-devel -y
curl --silent --location http://pkg.jenkins-ci.org/redhat-stable/jenkins.repo | sudo tee /etc/yum.repos.d/jenkins.repo
rpm --import https://jenkins-ci.org/redhat/jenkins-ci.org.key
yum install jenkins -y
yum install epel-release -y
yum install pylint -y
systemctl start jenkins
/sbin/chkconfig jenkins on
firewall-cmd --permanent --zone=public --add-port=8080/tcp
cat /var/lib/jenkins/secrets/initialAdminPassword
```

***2.GitHub plugin installation***
```
http://<Jenkins_IP>:8080/pluginManager/available
```
Find and install:

GitHub Integration Plugin

***3. GitHub global config***
This step provides an ability for Jenkins to create new web-hooks
```
http://<Jenkins_IP>:8080/configure
```
Go to GitHub section, add your credentials:
* Press "Advanced..."
* Press "Manage additional GitHub actions"
* Convert login and password to token


Go to GitHub Pull Requests section, fill the line Published Jenkins URL:
* ```http://<Jenkins_IP>:8080/```

***4. Pipeline how-to***

Create new pipeline:

* ```http://<Jenkins_IP>:8080/view/all/newJob ```
General:

Github project
* ```https://github.com/a1ex-var1amov/jenkins-test/``` (Use link to your github)

Build triggers
* GitHub hook trigger for GITScm polling

Pipeline

* Pipeline script from SCM
* SCM: GIT
* url: ```https://github.com/a1ex-var1amov/jenkins-test```
* your credentials
* script path:
Jenkinsfile

What in Jenkinsfile:
```
node {
  stage('Checkout') {
    checkout scm
    sh "ls -l"
  }
  stage('Syntax') {
    sh "pylint *.py"
  }
}


```
