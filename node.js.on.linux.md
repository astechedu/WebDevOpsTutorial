$$\color{purple}{NodeJs \ Npm \ React \ Vue \ Angular \ etc \ Installations}$$

<a name="top"></a>
Topics:

 1. [Install Node.js and npm from the Ubuntu repository](#nodejs_on_linux) <br>
 2. [Installing Node.js and npm from NodeSource](#nodejs_from_NodeSourceon_linux) <br>
 3. [Installing Node.js and npm using NVM](#nodejs_using_nvm_on_linux) <br>
 4. [Install NPM](#npm_on_linux) <br>
 5. [How to Install ReactJS on Ubuntu 20.04?](#react_on_linux)<br>
 6. [Install Vue.js in Ubuntu 20.04](#vue_on_linux)<br>
 7. [How to Install Angular CLI on Ubuntu 20.04](#angular_on_linux)<br>
    
  
  
  
  
 
[Go to Top](#top)
<a name="nodejs_on_linux">
# How To Install Node.js on Ubuntu 20.04

	sudo apt update
	sudo apt install nodejs
	
	OR
	
	sudo apt install nodejs npm
	
	node -v

	
	
	
	
	
[Go to Top](#top)
<a name="nodejs_from_NodeSourceon_linux">	
# Installing Node.js and npm from NodeSource	
	
NodeSource is a company focused on providing enterprise-grade Node support. It maintains an APT repository containing multiple Node.js versions. Use this repository if your application requires a specific version of Node.js.
	
	
	curl -fsSL https://deb.nodesource.com/setup_current.x | sudo -E bash - &&\
	sudo apt-get install -y nodejs
	
	OR
	
	curl -fsSL https://deb.nodesource.com/setup_lts.x | sudo -E bash - &&\
	sudo apt-get install -y nodejs
	
	OR
	
	curl -fsSL https://deb.nodesource.com/setup_18.x | sudo -E bash - &&\
	sudo apt-get install -y nodejs
	
	OR
	
	curl -sL https://deb.nodesource.com/setup_14.x | sudo -E bash -
	
	OR 	

	curl -sL https://deb.nodesource.com/setup_16.x | sudo bash -
	
	sudo apt install nodejs
	
	OR
	
	sudo apt-get install -y nodejs
	
	node --version
	npm --version
	
	sudo apt install build-essential
	
	

	
	
	
[Go to Top](#top)
<a name="nodejs_using_nvm_on_linux">		
# Installing Node.js and npm using NVM
	
NVM (Node Version Manager) is a bash script that allows you to manage multiple Node.js versions on a per-user basis. With NVM you can install and uninstall any Node.js version that you want to use or test.
	
	
        curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
	
	OR
	
	wget -qO- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.2/install.sh | bash
	
	


Running either of the above commands downloads a script and runs it. The script clones the nvm repository to ~/.nvm, and attempts to add the source lines from the snippet below to the correct profile file (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc).

	
	export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
	[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm

	
	
	The script will clone the project’s repository from Github to the ~/.nvm directory:
	
	
Output: 
	
	=> Close and reopen your terminal to start using nvm or run the following to use it now:

	export NVM_DIR="$HOME/.nvm"
	[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"                    # This loads nvm
	[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm bash_completion


	nvm --version
	nvm list-remote
	nvm install node
	
Output: 
		
	...
	Checksums matched!
	Now using node v14.2.0 (npm v6.14.4)
	Creating default alias: default -> node (-> v14.2.0)

	
	node --version
	
	
Let’s install two more versions, the latest LTS version and version 10.9.0:

	nvm install --lts
	nvm install 10.9.0

	
You can list the installed Node.js versions by typing:

	nvm ls	
	
	
	
Output: 
	
	>      v10.9.0
	       v12.16.3
		v14.2.0
	default -> node (-> v14.2.0)
	node -> stable (-> v14.2.0) (default)
	stable -> 14.2 (-> v14.2.0) (default)
	iojs -> N/A (default)
	unstable -> N/A (default)
	lts/* -> lts/erbium (-> v12.16.3)
	lts/argon -> v4.9.1 (-> N/A)
	lts/boron -> v6.17.1 (-> N/A)
	lts/carbon -> v8.17.0 (-> N/A)
	lts/dubnium -> v10.20.1 (-> N/A)
	lts/erbium -> v12.16.3

	
	nvm use 12.16.3
	
	nvm alias default 12.16.3
	
	
	
nvm allows you to quickly install and use different versions of node via the command line.

	
Example:

	 nvm use 16
	
Now using node v16.9.1 (npm v7.21.1)
	
	 node -v
	
v16.9.1
	
	 nvm use 14
	
Now using node v14.18.0 (npm v6.14.15)
	
	 node -v
	
v14.18.0
	
	 nvm install 12
	
Now using node v12.22.6 (npm v6.14.5)
	
	 node -v
	
v12.22.6	
	
	
	
	
	
	
	
	
	
	
[Go to Top](#top)
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
   
   
   
[Go to Top](#top)
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
   
   
   
   
   
[Go to Top](#top)
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
   
	  
	  
	  
	  
	  
[Go to Top](#top)
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
              
