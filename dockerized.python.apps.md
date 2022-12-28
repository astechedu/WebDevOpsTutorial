# Dockerized Python
:link:[Home](all-file-links.md)     


<a name="top"></a>  
Topics: 

  1. [Dockrized Python](#doc_python)<br>
  2. [Dockrized Django](#doc_django)<br>
  3. [Dockrized Flask](#doc_flash)<br>









[Go To Top](#top)
<a name="doc_python"></a>  



[Go To Top](#top)
<a name="doc_django"></a>  
# Django   (Worked)
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


# Showing Error

WARNING: Running pip as the 'root' user can result in broken permissions and conflicting behaviour with the system package manager. It is recommended to use a virtual environment instead: https://pip.pypa.io/warnings/venv

[notice] A new release of pip available: 22.3 -> 22.3.1
[notice] To update, run: pip install --upgrade pip







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














