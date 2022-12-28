# Dockerized Python
:link:[Home](all-file-links.md)     


<a name="top"></a>  
Topics: 

  1. [Dockrized Python](#doc_python)<br>
  2. [Dockrized Django (Worked)](#doc_django)<br>
  3. [Dockrized Flask](#doc_flash)<br>









[Go To Top](#top)
<a name="doc_python"></a>  








[Go To Top](#top)
<a name="doc_django"></a>  
# Django   (Worked)
   Install Django in local dir: 
      pip install django
   
   
Add the following content to the Dockerfile.

    FROM python:3.8

    RUN apt-get update \
      && apt-get install -y --no-install-recommends \
        #postgresql-client \
      && rm -rf /var/lib/apt/lists/*

    WORKDIR /usr/src/app
    COPY requirements.txt ./
    RUN pip install -r requirements.txt
    COPY . .

    EXPOSE 8000
    CMD ["python", "manage.py", "runserver", "0.0.0.0:8000"]


requirements.txt: 

  requiremasgiref==3.6.0
  backports.zoneinfo==0.2.1
  Django==4.1.4
  sqlparse==0.4.3
  ents.txt:


.dockerignore:

#Byte-compiled / optimized / DLL files
  __pycache__/

  **/migrations
  src/media
  src/db.sqlite3
  Procfile
  .git


#Building docker image:

    docker build . -t astechutube/sample-django-app

#Running Container:

    docker run --name django01 -p 8080:8000 -d astechutube/sample-django-app



#Pull this image from Docker Hub 
    docker pull astechutube/sample-django-app



So access the application at the address http://localhost:8080/


:end:









[Go To Top](#top)
<a name="doc_flash"></a>  


I don't like ignoring warnings, as one day you will oversee an important one.

Here is a good explanation on best docker practices with python. Search for Example with virtualenv and you'll find this:

# temp stage (Now Working)

      FROM python:3.9-slim as builder

      WORKDIR /app

      ENV PYTHONDONTWRITEBYTECODE 1
      ENV PYTHONUNBUFFERED 1

      RUN apt-get update && \
          apt-get install -y --no-install-recommends gcc

      RUN python -m venv /opt/venv
      ENV PATH="/opt/venv/bin:$PATH"

      COPY requirements.txt .
      RUN pip install -r requirements.txt


      # final stage
      FROM python:3.9-slim

      COPY --from=builder /opt/venv /opt/venv

      WORKDIR /app

      ENV PATH="/opt/venv/bin:$PATH"














