# Jenkin Pipeline Commands

[Home](#all-files-links.md)

<a name="top"></a>

<a name="bottom"></a>

Topics: 
      
[Jenkins Installation](#jenkins_installation)

[Install Jenkins On Ubuntu 20.04](#jenkins_install_ubuntu20.02)









			     Jenkin Pipeline: 

			   /             	  \
			  /                	   \               
	 Pipeline Plugings               Using Groovy Script
		   /                                \
		  /                                  \
	 Job-1   Job-2   Job-3   Job-4                \
	 Build   Text    QA      Deploy                \

						      Job-1     __ stage-1
						      Pipeline     Build
							       \
								\   
								 stage-2
							      \  Text
							       \
								stage-3
							    \   QA
							     \
							      stage-4
							      Deploy




Using Groovy Script:

1) Scripted Pipeline
2) Declarative Pipeline  (New mostly being used)

------------------------------------------


1) Scripted Pipeline


	node{

		stage["build"]{
			echo "Welcome to Build Stage"
		}

		stage["Text"]{
			echo "Welcome to Build Stage"
		}

		stage["QA"]{
			echo "Welcome to Build Stage"
		}

		stage["Deploy"]{
			echo "Welcome to Build Stage"
		}

	}


------------------------------------------



2) Decripted Pipeline



	pipeline{

		agent any	
		stages{

			stage{"build"}{

				steps{
				  echo "Welcome to Build Stage";
				}
			}

			stage{"Test"}{

				steps{
				  echo "Welcome to Test Stage";
				}
			}

			stage{"QA"}{

				steps{
				  echo "Welcome to Test Stage";
				}
			}

			stage{"Deploy"}{

				steps{
				  echo "Welcome to Test Stage";
				}
			}				

		}

	}


-----------------------------------------------------------------------------------------------------


>>>> Jenkins Notes <<<<<<<<<<<



Jenkins initial setup is required. An admin user has been created and a password generated.
Please use the following password to proceed to installation:

cdc3d4d3881f4077a6adeb0ac57abe97

This may also be found at: 


		C:\Users\Ajay\.jenkins\secrets\initialAdminPassword


   		java -jar D:\Softwares\jenkin\jenkins.war  //Type in cmd to start jenkins



Type On Browser: 


	127.0.0.1:8080    //Type of Browser's address bar


Software:  Jenkins, Terraform, Kubernetes, Git, Docker 



Gaurav Sharma:


In Jenkins: 

  myproject-build
  myproject-test
  myproject-deploy
  myproject-deploy-prod



------------------------------------------------------------
------------------------------------------------------------
------------------------------------------------------------

>>>>>> Pipeline Script <<<<<<<<<


There are two types of pipelines in Jenkins:

1.   Declarative
2.   Scripted


Jenkins Pipeline Concepts:


	1.
		pipeline{  
		}  

	2.
		node{  
		}  



	    pipeline {  
		agent any  
		stages {  
			stage ('Build') {  
			    ...  
			}  
			stage ('Test') {  
			    ...  
			}  
			stage ('QA') {  
			    ...  
			}  
			stage ('Deploy') {  
			    ...  
			}  
			stage ('Monitor') {  
			    ...  
			}  
		}  
	    }  



----------------


Step: A step is a single task that executes a specific process at a defined time. A pipeline involves a series of steps defined within a stage block.


	    pipeline {  
		agent any  
		stages {  
			stage ('Build') {  
			    steps {  
				    echo 'Running build phase...'  
			    }  
			}  
		}  
	    }  



------------------



------------------------------------------------------------
------------------------------------------------------------




[Got To Top](#top)
<a name="jenkins_installation"></a>
# How To Install Jenkins on Ubuntu 20.04


Introduction

When faced with repetitive technical tasks, finding automation solutions that work can be a chore. With Jenkins, an open-source automation server, you can efficiently manage tasks from building to deploying software. Jenkins is Java-based, installed from Ubuntu packages or by downloading and running its web application archive (WAR) file — a collection of files that make up a complete web application to run on a server.

In this tutorial we’ll install Jenkins on Ubuntu 20.04, start the development server and create an administrative user to get you started in exploring what Jenkins can do. While you’ll have a development-level server ready for use at the conclusion of this tutorial, to secure this installation for production, follow the guide How to Configure Jenkins with SSL Using an Nginx Reverse Proxy on Ubuntu 18.04.
Prerequisites

To follow this tutorial, you will need:

    One Ubuntu 20.04 server configured with a non-root sudo user and firewall by following the Ubuntu 20.04 initial server setup guide. We recommend starting with at least 1 GB of RAM. Visit Jenkins’s “Hardware Recommendations” for guidance in planning the capacity of a production-level Jenkins installation.
    Oracle JDK 11 installed, following our guidelines on installing specific versions of OpenJDK on Ubuntu 20.04.

Step 1 — Installing Jenkins:

The version of Jenkins included with the default Ubuntu packages is often behind the latest available version from the project itself. To ensure you have the latest fixes and features, use the project-maintained packages to install Jenkins.

First, add the repository key to the system:



   	      wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -



After the key is added the system will return with OK.

Next, let’s append the Debian package repository address to the server’s sources.list:

    sudo sh -c 'echo deb http://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

After both commands have been entered, we’ll run update so that apt will use the new repository.



    		sudo apt update




Finally, we’ll install Jenkins and its dependencies.



                  sudo apt install jenkins




Now that Jenkins and its dependencies are in place, we’ll start the Jenkins server.
Step 2 — Starting Jenkins

Let’s start Jenkins by using systemctl:



		sudo systemctl start jenkins



Since systemctl doesn’t display status output, we’ll use the status command to verify that Jenkins started successfully:



    		sudo systemctl status jenkins



If everything went well, the beginning of the status output shows that the service is active and configured to start at boot:

Output

● jenkins.service - LSB: Start Jenkins at boot time
   Loaded: loaded (/etc/init.d/jenkins; generated)
   Active: active (exited) since Fri 2020-06-05 21:21:46 UTC; 45s ago
     Docs: man:systemd-sysv-generator(8)
    Tasks: 0 (limit: 1137)
   CGroup: /system.slice/jenkins.service


Now that Jenkins is up and running, let’s adjust our firewall rules so that we can reach it from a web browser to complete the initial setup.


Step 3 — Opening the Firewall:

To set up a UFW firewall, visit Initial Server Setup with Ubuntu 20.04, Step 4- Setting up a Basic Firewall. By default, Jenkins runs on port 8080. We’ll open that port using ufw:


    		sudo ufw allow 8080



Note: If the firewall is inactive, the following commands will allow OpenSSH and enable the firewall:


		  sudo ufw allow OpenSSH
		  sudo ufw enable


Check ufw’s status to confirm the new rules:


    		   sudo ufw status


You’ll notice that traffic is allowed to port 8080 from anywhere:

Output

Status: active

To                         Action      From
--                         ------      ----
OpenSSH                    ALLOW       Anywhere
8080                       ALLOW       Anywhere
OpenSSH (v6)               ALLOW       Anywhere (v6)
8080 (v6)                  ALLOW       Anywhere (v6)


With Jenkins installed and our firewall configured, we can complete the installation stage and dive into Jenkins setup.


Step 4 — Setting Up Jenkins:


To set up your installation, visit Jenkins on its default port, 8080, using your server domain name or IP address: http://your_server_ip_or_domain:8080

You should receive the Unlock Jenkins screen, which displays the location of the initial password:

Unlock Jenkins screen




In the terminal window, use the cat command to display the password:



    		sudo cat /var/lib/jenkins/secrets/initialAdminPassword




Copy the 32-character alphanumeric password from the terminal and paste it into the Administrator password field, then click Continue.

The next screen presents the option of installing suggested plugins or selecting specific plugins:

Customize Jenkins Screen

We’ll click the Install suggested plugins option, which will immediately begin the installation process.


Jenkins Getting Started Install Plugins Screen

When the installation is complete, you’ll be prompted to set up the first administrative user. It’s possible to skip this step and continue as admin using the initial password we used above, but we’ll take a moment to create the user.

Note: The default Jenkins server is NOT encrypted, so the data submitted with this form is not protected. Refer to How to Configure Jenkins with SSL Using an Nginx Reverse Proxy on Ubuntu 20.04 to protect user credentials and information about builds that are transmitted via the web interface.

Jenkins Create First Admin User Screen

Enter the name and password for your user:



Jenkins Create User:

You’ll receive an Instance Configuration page that will ask you to confirm the preferred URL for your Jenkins instance. Confirm either the domain name for your server or your server’s IP address:


Jenkins Instance Configuration:

After confirming the appropriate information, click Save and Finish. You’ll receive a confirmation page confirming that “Jenkins is Ready!”:

Jenkins is ready screen

Click Start using Jenkins to visit the main Jenkins dashboard:

Welcome to Jenkins Screen

At this point, you have completed a successful installation of Jenkins.





:end:




[Go To Top](#top)
<a name="jenkins_install_ubuntu20.04"></a>
# How to install Jenkins on Ubuntu 20.04

The steps followed and the commands used to install Jenkins on Ubuntu 20 are as follows:

    sudo apt-get update

    sudo apt-get install openjdk-8-jdk

    wget -q -O - https://pkg.jenkins.io/debian-stable/jenkins.io.key | sudo apt-key add -

    sudo sh -c 'echo deb https://pkg.jenkins.io/debian-stable binary/ > /etc/apt/sources.list.d/jenkins.list'

    sudo apt-get update

    sudo apt-get install jenkins

    sudo apt install git



:end:










