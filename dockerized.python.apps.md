# Dockerized Python
:link:[Home](all-file-links.md)     


<a name="top"></a>  
Topics: 

  1. [Dockrized Python](#doc_python)<br>
  2. [Dockrized Django](#doc_django)<br>
  3. [Dockrized Python](#doc_flash)<br>









[Go To Top](#top)
<a name="doc_python"></a>  



[Go To Top](#top)
<a name="doc_django"></a>  

Add the following content to the Dockerfile.

      # syntax=docker/dockerfile:1
      FROM python:3
      ENV PYTHONDONTWRITEBYTECODE=1
      ENV PYTHONUNBUFFERED=1
      WORKDIR /code
      COPY requirements.txt /code/
      RUN pip install -r requirements.txt
      COPY . /code/




Add the required software in the file.

      Django>=3.0,<4.0
      psycopg2>=2.8

Save and close the requirements.txt file.


    services:
      db:
        image: postgres
        volumes:
          - ./data/db:/var/lib/postgresql/data
        environment:
          - POSTGRES_DB=postgres
          - POSTGRES_USER=postgres
          - POSTGRES_PASSWORD=postgres
      web:
        build: .
        command: python manage.py runserver 0.0.0.0:8000
        volumes:
          - .:/code
        ports:
          - "8000:8000"
        environment:
          - POSTGRES_NAME=postgres
          - POSTGRES_USER=postgres
          - POSTGRES_PASSWORD=postgres
        depends_on:
          - db







[Go To Top](#top)
<a name="doc_flash"></a>  
