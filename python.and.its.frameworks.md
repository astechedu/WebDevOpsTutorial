$$\color{purple}{Python \ And \ Its \ Framworks \ Installations}$$

<a name="top"></a>
Topics:

 1. [How To Install Python 3 and Set Up a Programming Environment on an Ubuntu 20.04 Server](#python_on_linux)
 2. [Install NPM](#django_on_linux)
 3. [Install React App](#flash_on_linux)
  
  
  
  
  
  [Go to Top](#top)
  <a name="python_on_linux">
  # How To Install Python 3 and Set Up a Programming Environment on an Ubuntu 20.04 Server
 
 
 Setting Up Python 3: 
 
     sudo apt update
     sudo apt -y upgrade
     python3 -V

     sudo apt install -y python3-pip
     pip3 install package_name
     sudo apt install -y build-essential libssl-dev libffi-dev python3-dev

 
 Setting Up a Virtual Environment: 
 
      sudo apt install -y python3-venv
      mkdir environments
      cd environments
      python3 -m venv my_env
      ls my_env
      source source my_env/bin/activate
      (my_env) ajay@sisaudiya:~/environment$
 
 Creating a “Hello, World” Program: 
 
       (my_env) ajay@sisaudiya:~/environment$ nano hello.py
 
 
  hello.py

        print("Hello, World!")
        (my_env) ajay@sisaudiya:~/environment$python hello.py
 
 
 
 
 
 
 
 
 
  [Go to Top](#nodejs_on_linux)
  <a name="django_on_linux">
  # Install NPM on Ubuntu 20.04
   
   
   
  [Go to Top](#nodejs_on_linux)
  <a name="flash_on_linux">
  # Install React App On Ubuntu 20.04
   
   
 :end:
              
