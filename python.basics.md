# Python Basics For Beginners


### Topics

  [Creating Virtual environment click here](#virtual_env) <br />





<a name="virtual_env"></a>
#### Python 3.8 Installation on Ubuntu 20.04: 

Step 1: Update and Refresh Repository Lists


	sudo apt update
	
	
Step 2: Install Supporting Software


	sudo apt install software-properties-common
	
	
Step 3: Add Deadsnakes PPA	

	
	sudo add-apt-repository ppa:deadsnakes/ppa
	sudo apt update
	
	
Step 4: Install Python 3.8 : 


	sudo apt install python3.8
	python3 --version	
	
	
Step 5: Installing venv 

        sudo apt install python3.8-env
	
Step 6: Creating new directory

        mkdir project01
        cd project01
	
Output: 

	ajay@sisaudiya:~/project01$
	
	
Step 7: Creating Virtual Environments

        ajay@sisaudiya:~/project01$ python3 -m venv env01
        

             
Step 8: Activating the virtual environment

         ajay@sisaudiya:~/project01$ env01/bin/activate  


Output: 

       (env01) ajay@sisaudiya:~/project01$
       
       
Step 9: To deactivate a virtual environment

	 ajay@sisaudiya:~/project01$ deactivate  

Output: 

       ajay@sisaudiya:~/project01$ 
