<h1>Launching Jenkins from Dockerfile and Deploy-Monitor-Test</h1>
<h1>Task Overview:</h1>
<ol>
<li>Create Container image that has Jenkins installed using dockerfile.</li>
<li>When we launch this image, it should automatically starts Jenkins service in the container.</li>
<li>Create a job chain of Job1, Job2, Job3 using build pipeline plugin in Jenkins.</li.
<li>JOB1: Pull the Github repo automatically when some developers push repo to Github.</li>
<li> JOB2: Test your app wheateher working or not.</li>
<li> JOB3: If the app is not working than automatically start the containner again.</li>
</ol>

<h2>Software Required:</h2>
<ol>
<li>Github</li>
<li>Jenkins</li>
<li>Docker</li>
</ol>

<h2>Project Description</h2>
<h3>Creating Dockerfile for Jenkins</h3>
 
![dockerfile](https://raw.githubusercontent.com/yashbajpai98/task2LW/master/task2-images/dockerfile.PNG)

Now, Build Image: docker build -t jenkins:v1
 ![3](https://raw.githubusercontent.com/yashbajpai98/task2LW/master/task2-images/3.PNG)
 
Now, Launch a new container through this image of jenkins:v1 so that jenkins get automatically launched.
 ![4](https://raw.githubusercontent.com/yashbajpai98/task2LW/master/task2-images/4.PNG)
 
 --privileged : is used to give special access to run docker commands in host OS through jenkins server.

-v /:/host : mounting is done for this reason only.

-p 9999:8080 :  by exposing port we can access Jenkins server from http://localhost:9999
For first time Jenkins will ask an Initial Admin Password which we can find in the running jenkins container :

 ![5](https://raw.githubusercontent.com/yashbajpai98/task2LW/master/task2-images/5.PNG)
 ![6](https://raw.githubusercontent.com/yashbajpai98/task2LW/master/task2-images/6.PNG)
 
 <h3>Job1(Copy Github Code)</h3> :

Whenever Developer pushes something new in Github, Job1 coppies the code from Github to a directory inside the Jenkins server container.
 ![job1](https://raw.githubusercontent.com/yashbajpai98/task2LW/master/task2-images/job1.PNG)
 
<h3> Job2(Deploy Container) :</h3>

Successful build of Job1 will trigger Job2 and it will launch the recpective container for the code of the developer. Here I have taken example of webpages so I have used apache webserver.
 ![job2](https://raw.githubusercontent.com/yashbajpai98/task2LW/master/task2-images/job2.PNG)

<h3>Job3(Testing Container) :</h3>

After successful build of Job2 will trigger Job3 and it tests if the deployed container is working or not.It will be successfully built if the deployed container fails and then trigger Job4 for giving notification to the developer.
 ![job3](https://raw.githubusercontent.com/yashbajpai98/task2LW/master/task2-images/job3.PNG)
 If this fails then it again runs the job2.
 

