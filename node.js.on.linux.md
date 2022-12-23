$$\color{purple}{NodeJs \ Npm \ React \ Vue \ Angular \ etc \ Installations}$$
:
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
# 1. How To Install Node.js on Ubuntu 20.04

	sudo apt update
	sudo apt install nodejs
	
	OR
	
	sudo apt install nodejs npm
	
	node -v

	
	
	
	
	
[Go to Top](#top)
<a name="nodejs_from_NodeSourceon_linux">	
# 2. Installing Node.js and npm from NodeSource	
	
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
	
	

	
### Uninstall nodejs Ubuntu & Debian packages

To completely remove Node.js installed from the deb.nodesource.com package methods above:
use sudo on Ubuntu or run this as root on debian

	apt-get purge nodejs &&\
	rm -r /etc/apt/sources.list.d/nodesource.list	
	
	

#### Manual installation

If you're not a fan of curl <url> | bash -, or are using an unsupported distribution, you can try a manual installation.

These instructions assume sudo is present, however some distributions do not include this command by default, particularly those focused on a minimal environment. In this case, you should install sudo or su to root to run the commands directly.

       1. Remove the old PPA if it exists

This step is only required if you previously used Chris Lea's Node.js PPA.

	# add-apt-repository may not be present on some Ubuntu releases:
	# sudo apt-get install python-software-properties
	sudo add-apt-repository -y -r ppa:chris-lea/node.js &&\
	sudo rm -f /etc/apt/sources.list.d/chris-lea-node_js-*.list &&\
	sudo rm -f /etc/apt/sources.list.d/chris-lea-node_js-*.list.save

	
        2. Add the NodeSource package signing key

	KEYRING=/usr/share/keyrings/nodesource.gpg
	curl -fsSL https://deb.nodesource.com/gpgkey/nodesource.gpg.key | gpg --dearmor | sudo tee "$KEYRING" >/dev/null
	# wget can also be used:
	# wget --quiet -O - https://deb.nodesource.com/gpgkey/nodesource.gpg.key | gpg --dearmor | sudo tee "$KEYRING" >/dev/null
	gpg --no-default-keyring --keyring "$KEYRING" --list-keys

	
The key ID is 9FD3B784BC1C6FC31A8A0A1C1655A0AB68576280.

	
        3. Add the desired NodeSource repository

# Replace with the branch of Node.js or io.js you want to install: node_8.x, node_16.x, etc...
	
	VERSION=node_16.x
	# Replace with the keyring above, if different
	KEYRING=/usr/share/keyrings/nodesource.gpg
	# The below command will set this correctly, but if lsb_release isn't available, you can set it manually:
	# - For Debian distributions: jessie, sid, etc...
	# - For Ubuntu distributions: xenial, bionic, etc...
	# - For Debian or Ubuntu derived distributions your best option is to use the codename corresponding to the upstream release your distribution is based off. This is an advanced scenario and unsupported if your distribution is not listed as supported per earlier in this README.
	
	DISTRO="$(lsb_release -s -c)"
	echo "deb [signed-by=$KEYRING] https://deb.nodesource.com/$VERSION $DISTRO main" | sudo tee /etc/apt/sources.list.d/nodesource.list
	echo "deb-src [signed-by=$KEYRING] https://deb.nodesource.com/$VERSION $DISTRO main" | sudo tee -a /etc/apt/sources.list.d/nodesource.list

        4. Update package lists and install Node.js

	sudo apt-get update
	sudo apt-get install nodejs
	
	
	
	
	
	
	
	
[Go to Top](#top)
<a name="nodejs_using_nvm_on_linux">		
# 3. Installing Node.js and npm using NVM
	
     Installing and Updating:
	
	
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


	
	Confirm you have successfully installed NVM.

        command -v nvm
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
	
	
	
    #### Use NVM to Install Node
	
	nvm install node
	nvm ls-remote
	
	nvm install 13.10.1 # Specific minor release
	nvm install 14 # Specify major release only	
	
	
    #### List Node Versions with NVM	
	
	nvm ls
	
    #### The NVM Use Command
	
	nvm use node
	
	or

	nvm use 14

	nvm current
	
	
     #### NVM: Switch Node Version	
	
	nvm run node

	
     #### Creating NVM Aliases
	
	
	nvm alias default 14
	nvm alias maintenance 13.10.1
	nvm ls

	
     #### Use NVM to Install Latest LTS Node.js Release
	
	
	nvm install --lts
	nvm install --lts=argon
	nvm use --lts
	nvm use lts/argon	
	
	
      #### Additional NVM Capabilities
	
	nvm install node --reinstall-packages-from=default
	nvm set-colors rgBcm
	
	
      #### Use NVM to Uninstall Node
	
	nvm uninstall 13.10.1
	Uninstalled node v13.10.1
	
      #### NVM Uninstall Steps
       
	nvm deactivate
	nvm unload
	
	
       Clean up your .bashrc file by removing the following lines:
	
	
	export NVM_DIR="$HOME/.nvm"
	[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh"  # This loads nvm
	[ -s "$NVM_DIR/bash_completion" ] && \. "$NVM_DIR/bash_completion"  # This loads nvm	
	
	
	
	
	
	
	
	
	
	
[Go to Top](#top)
<a name="npm_on_linux">
# 4. Install NPM on Ubuntu 20.04
   
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
# 5. Install React App On Ubuntu 20.04
   

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
# 6. Install Vue Js On Ubuntu 20.04

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
# 7. How to Install Angular CLI on Ubuntu 20.04:


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

	ng --version
	ng new hello-world
	cd hello-world
	ng serve 	
	ng serve --host 0.0.0.0 --port 8080 	
   
	  
	  
	  
	  
   
 :end:
              
