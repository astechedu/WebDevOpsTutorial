$$\color{purple}{Python \ And \ Its \ Framworks \ Installations}$$
:link:[Home](all-file-links.md)     





<a name="top"></a>
Topics:

 1. [How To Install Python 3 and Set Up a Programming Environment on an Ubuntu 20.04 Server](#python_on_linux) <br>
 2. [How to Install virtualenv on Ubuntu 20.04 LTS (Focal Fossa)](#venv_on_linux) <br>
 3. [How To Install the Django Web Framework on Ubuntu 20.04](#django_on_linux) <br>
 4. [How To Install the Flask Web Framework on Ubuntu 20.04](#flash_on_linux) <br>
  
  
  
  
  
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
 
 
 
 
 
 
 
 
 
  [Go to Top](#top)
  <a name="venv_on_linux">
  # How to Install virtualenv on Ubuntu 20.04 LTS (Focal Fossa)
   
   Update Your Server:
   
        sudo apt update
        sudo apt upgrade

   Install pip3:
   
         sudo apt install python3-pip
   
   Install virtualenv:
   
          pip3 install virtualenv
   
   Check Version: 
   
       virtualenv --version
   
   Create a Virtual environment: 
          
        virtualenv venv
   
   Activate or Deactivate environment: 
   
         ajay@sisaudiya:~$ source venv/bin/activate
         (venv) ajay@sisaudiya:~$
   
         (venv) ajay@sisaudiya:~$ deactivate
         ajay@sisaudiya:~$


   
   
   
   
  [Go to Top](#nodejs_on_linux)
  <a name="django_on_linux">
  # Install Django App On Ubuntu 20.04
   
     Installed Python: 
   
         python -v
   
      Django: 
   
       sudo apt install python3-django
       django-admin --version
   
   
   
Install with pip in a Virtual Environment: 
   
        sudo apt update
        python3 -V
        sudo apt install python3-pip python3-venv
        mkdir ~/newproject
        cd ~/newproject
        python3 -m venv my_env
        source my_env/bin/activate
        (my_env) ajay@sisaudiya:~/myapp$ pip install django
        (my_env) ajay@sisaudiya:~/myapp$ django-admin --version
        (my_env) ajay@sisaudiya:~/myapp$ deactivate
        cd ~/newproject
        source my_env/bin/activate
   
   
Development Version Install with Git:
   
       sudo apt update
       python3 -V
   
       sudo apt install python3-pip python3-venv
       git clone git://github.com/django/django ~/django-dev
       cd ~/django-dev
       python3 -m venv my_env
       source my_env/bin/activate
       (my_env)$ pip install -e ~/django-dev
       django-admin --version
   
Creating a Sample Project: 
   
   
        mkdir ~/django-test
        cd ~/django-test 
        python3 -m venv my_env
        source my_env/bin/activate
        (my_env)$ pip install django
        (my_env)$ django-admin startproject djangoproject .
        (my_env)$ python manage.py migrate       
        (my_env)$ python manage.py createsuperuser
   
   
Modifying ALLOWED_HOSTS in the Django Settings:
   
    (my_env)$ nano ~/django-test/djangoproject/settings.py
   
   
   
~/django-test/djangoproject/settings.py

ALLOWED_HOSTS = ['your_server_ip_or_domain', 'your_second_ip_or_domain', . . .]

Testing the Development Server: 
      
     
    (my_env)$ sudo ufw allow 8000
    (my_env)$ python manage.py runserver your_server_ip:8000
    http://your_server_ip:8000
   
   
   
   
    
   
   
   
   
   
 :end:
              
