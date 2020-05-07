# DevOps_Automation_Project-

## This is a project on DevOps Assembly Line for end to end automation from developer to client, In this project I have used technologies like Jenkins, Github, Docker, Linux.
### About Project
   * Here I have created three different jobs in jenkins each having its own task to do and each one of them is completely automatic. So Job 1 is of production system. This job will keep an eye on master branch, means that if any developer in the company merges his code in the master branch then the system will automatically do all the things first of all it will check whether our webserver is ready, if not it will launch a fresh new webserver and that automatically and then will expose website for clients. 
   * Now, Job 2 is basically a Testing system this job will also keep an eye on a branch but now not on master but on developer branch, It will keep on tracking this branch as soon as developer commits anything it will deploy it on Testing server. 
   * Then comes the role of Job 3 . It is there to wait, wait until gets a trigger or certificate from Quality Assurance team that whatever we have on this branch is working properly. After getting a certificate it will merge the developer branch to master and push everything there and this process continuous. So This is all about this project . . . Let me share my journey and experiece troughout the journey of this project.

### Requirements
* Base OS (I have RHEL 8 as a VM)
* Docker
* Jenkins and JDK
* Git
* ngrok

### Procedure
# 1. Git and Github setup
  I am having RHEL as my base OS, I have installed git in this OS so that my developer can have facility of Version Contolling.

`yum install git`
* Github Configuration : I have created an github public repository initializing readme along, this will be my remote system where I will deploy my code. 

* Git Configuration : I have created two local repositories one with the name master and other with developer both having their own functionality as I mentioned earlier I have also updated both the branches over remote repository. 
`git push --set-upstream origin developer`

git push --set-upstream origin developer
After this configuration I made first automation by adding post-commit file in hooks of git so that as soon as developer hit commit it will automatically get pushed to remote repository.
This is all about Git and Github configuration.

# 2. Building Production System
Here I have started with the first automatic job of jenkins. This job will triggered by manipulation of master branch.

https://github.com/ajinkya48765/DevOps_Automation_Project-/blob/master/code_snippet%20job1

# 3. Docker setup
* I have installed latest version of docker in my machine I am using docker-ce.
* I have also created my own webserver and created image named httpd. We have to take into consideration three cases before running this os I have provided Screenshot for the reference
* If we are running this OS for the first time - we will just run this os with all the options like patting, volume, name.
`sudo docker run -dti --name server -v auto:/var/www/html -p 7081:80 httpd`
                                                             
* If we have the container but is stopped - This caser can be determined by running docker ps -a | grep <container name> if container is present it will return True then we will just start it again .
`sudo docker start server`

* If our container is already running we will just run this block empty.
`echo "already running"`

* I have provided integration of all the commands in the below snippet.

   https://github.com/ajinkya48765/DevOps_Automation_Project-/blob/master/code_snippet%20job1


# 4. Testing System
* In the testing system my requirenment was to keep checking developer branch if any manupulation found I just have to send all the data to testing server to my testing team, They will test everything there.

* For this I have created exactly same server as I have created for production so that there should not be any kind of version mismatch 

* In this job I have to keep an eye on developer branch so I have added here (Branch Specifier) developer.


As we did in Job here also we have to consider all those things.

* Till now we are so much clear that we have provided our code to testing team and they are testing it but what after they are sure that this is safe and sound website. Hence we have our third job

# 5. Quality Assurance Certificate
* Till here we have our master branch ready our developer branch ready but we don't have link which will connect developer branch to master.
* Here I have added my github here in this job. Here the main thing is that we have to provide credentials like our user id and password.
* we have added module called merge before build we have to add here name of repository , name of our branch etc.
* I have also used git publisher here for post build operations here I will push my code from developer branch to master.



## In this way I have created my whole project Thank you so much Mr. Vimal Daga sir for your guidance.
