# empirix-sample-java-project

The repository contains a simple Java application which outputs the string
"Hello world!" and is accompanied by a couple of unit tests to check that the
main application works as expected. The results of these tests are saved to a
JUnit XML report.




1. This project can be used with jenkins setup to run and build a java project. 

2. Below plugins were used and required to be installed on jenkins to run this project on jenkins. 

*Git webhook plugin  
*build timestamp plugin
*copy artifact plugin
*git
*github branch source plugin
*github integration plugin
*github plugin
*junit plugin
*parameterized trigger plugin
*All pipeline plugins

UNder global configuration : Enable BUILD_TIMESTAMP checkbox with format of timestamp required. 

3. Once plugins installed, create a pipeline job on jenkins and in GITHUB project option, provide your repo url. 

4. Under build trigger, enable the option "GITHUB hook trigger for GITscm polling". Before this step GITHUB webhook integration should be done with jenkins as per below steps. 

add a webhook in GitHub and then add this webhook in Jenkins.

	a) Go to your project repository.
	b) Go to "settings" in the right corner.
	c) Click on "webhooks."
	d) Click "Add webhooks."
	e) Write the Payload URL as "https://jenkins-server.com/github-webhook/"

Here, Payload URL is the URL where our Jenkins is running add github-webhook to tell GitHub that it is a webhook.

	Content type: What kind of data we want in our webhook. I have selected JSON data.
	Secret: Used to secure our webhook we can provide a secret in our webhook and ensure that only applications having this webhooks can use it.
	SSL verification: This SSL Checker will help you diagnose problems with your SSL certificate installation. You can verify the SSL certificate on your web server to make sure it is correctly installed, valid, trusted and doesn’t give any errors to any of your users.
	
	Which events would you like to trigger this webhook?
	Options: 
	Just the push event: Only send data when someone pushed into my repository.
	Send me everything: If there is any pull or push event in our repository we will get notified.
	Let me select individual events: We can configure for what events we want our data.
	
Click Create and a webhook will be created.

	To use this webhook in Jenkins.

	a) Go to Manage Jenkins -> Configure System
	b) Scroll down and you will find the GitHub Pull Requests checkbox. In the Published Jenkins URL, add the repository link
		Click on "Save."

5. Once done, select the "Pipeline Script from SCM "option under pipeline section in jenkins. 
		Give repo URL and branch specifier as /Master. 
		Scriptpath : Jenkinsfile. 
		
		
		
OUTPUT OF THE PROJECT: 
Whenever there is any push in the GIT master branch, the pipeline job will be triggered and the latest build will be copied to the provided path which is set to /tmp as default if no input provided. Artifact will be saved inside a directory created with timestamp. 

All stages output will be shown on the pipeline view inside job with all the stages completed: 
	1st : CheckoutSCM
	2nd : Tool Install
	3rd : Build
	4th : Test
	5th : Deploy
	6th : Post Actions

