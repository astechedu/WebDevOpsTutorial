# Node js
#$\color{purple}{Node Js Npm React Vue Angular etc. Installations}$$

<a name="top"></a>
Topics:

 1. [How To Install Node.js on Ubuntu 20.04](#nodejs_on_linux) <br>
 2. [Install NPM](#npm_on_linux) <br>
 3. [How to Install ReactJS on Ubuntu 20.04?](#react_on_linux)<br>
 4. [Install Vue.js in Ubuntu 20.04](#vue_on_linux)<br>
 5. [How to Install Angular CLI on Ubuntu 20.04](#angular_on_linux)<br>
    
  
  
  [Go to Top](#nodejs_on_linux)
  <a name="nodejs_on_linux">
# How To Install Node.js on Ubuntu 20.04

      sudo apt update
      sudo apt install nodejs
      node -v
 
 
 
  [Go to Top](#nodejs_on_linux)
  <a name="npm_on_linux">
# Install NPM on Ubuntu 20.04
   
       sudo apt update
       sudo apt install npm
   
 Installing Node.js with Apt Using a NodeSource PPA
   

        cd ~
        curl -sL https://deb.nodesource.com/setup_16.x -o /tmp/nodesource_setup.sh
        nano /tmp/nodesource_setup.sh
        sudo bash /tmp/nodesource_setup.sh   
        sudo apt install nodejs
        node -v
   
   
   
   
  [Go to Top](#nodejs_on_linux)
  <a name="react_on_linux">
# Install React App On Ubuntu 20.04
   

How to Install ReactJS on Ubuntu 20.04?


Installing NPM:

	sudo apt install npm
        npm --version
        
        node --version
        
        
        
Install Create-React-App tool: 

	sudo npm -g install create-react-app
        create-react-app --version
        
        
        create-react-app appName
        
        cd appName
        
        
        npm start
        
        
 And your browser will open-up and shows you that the app is up and running with local host-3000
   
   
   
   
   
  [Go to Top](#nodejs_on_linux)
  <a name="vue_on_linux">
# Install Vue Js On Ubuntu 20.04

 Install Vue.js in Ubuntu 20.04:
 
 
 
 
 Installation: 
 
 Using the CDN Package:
 
 <script src="https://unpkg.com/vue@next"></script></td>
 
 
 
Using NPM: 

	#latest stable
	npm install vue@next
	 
	 
 
 Using CLI: 
 
 	sudo yarn global add @vue/cli
	# OR
 	sudo npm install -g @vue/cli
 
 
 	vue --version
 
 
If you want to upgrade to the latest stable version of Vue.js: 

	 sudo yarn global upgrade --latest @vue/cli
	 # OR
	 sudo npm update -g @vue/cli 
	 
 
 Getting started with Vue.js: 
 
 	vue create demo-app
 	vue ui
   
	  
	  
	  
	  
	  
  [Go to Top](#nodejs_on_linux)
  <a name="angular_on_linux">
# How to Install Angular CLI on Ubuntu 20.04:


Installing Node.js:


curl https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash 

	source ~/.bashrc
	nvm install node


 Installing Angular CLI:
 
 	npm install -g @angular/cli
 	
 	
 

 You may require older Angular version on your machine. To install specific Angular version run command as following with version number.

	npm install -g @angular/cli@8        #Angular 8
	npm install -g @angular/cli@9        #Angular 9
	npm install -g @angular/cli@10       #Angular 10
		
	 	
Creating New Angular Application: 

	cd hello-world
	ng serve 	
	ng serve --host 0.0.0.0 --port 8080 	
   
	  
	  
	  
	  
   
 :end:
              
