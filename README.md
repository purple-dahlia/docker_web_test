
# docker_web_test
Devops Assembly Lines Day8 git-jenkins-webserver integration homework

<h1> Automate deployment to a webserver

<h5> Task Description

The purpose of this project is automate the deployment of HTML pages in a remote webserver running on Docker. Here the machine is in AWS cloud, and the webserver is the base image of httpd. Both the dev and the prod webservers are running on the same machine, but in different containers - dev_dock and prod_dock respectively. Steps to implement and the corresponding tasks in Je nkins:

* **Task 1** - As soon as the developer does a commit (with git commit)
  * Code should be pushed to git DEV branch - bash post-commit hook
  * A job is triggered in jenkins - also via the post-commit hook,through a CURL command
    * The task of this job is to download the code from GIT, and copy the html files to /home/ec2-user/dev_web location on the remote machine, which has been volume mapped to /usr/local/apache2/htdocs of dev_dock container
    * QA will test with the dev server URL http://ec2-18-221-114-170.us-east-2.compute.amazonaws.com:8081
    * The name of the jenkins job is docker_dev_deploy
  
* **Task 2** - After QA signs off on the dev environment, a second jenkins job, called docker_merge, should be run, which merges the changes of DEV branch to the master, pushes the master to github, and triggers another jenkins job,

* **Task 3** - The name of this job is docker_prod_deploy, and its task is to copy the newly made changes to the master branch into /home/ec2-user/prod_web location on the remote machine, which has been volume mapped to /usr/local/apache2/htdocs of the prod_dock container
  * The production URL is http://ec2-18-221-114-170.us-east-2.compute.amazonaws.com:8080

The whole setup can be done on a local machine too, but my laptop is a little ancient, and could not handle both running the VM and jenkins and kept crashing, so I moved the containers and webservers to AWS


