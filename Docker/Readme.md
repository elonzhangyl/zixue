1. Run docker containers locally
    1. In the work directory of your local machine, create *Dockerfile* with the content below: 
```
FROM python:3.8
# Setup env
ENV PYTHONDONTWRITEBYTECODE=1
ENV PYTHONFAULTHANDLER=1
WORKDIR /code
# Install & use pipenv
COPY Pipfile Pipfile.lock /code/
RUN python -m pip install --upgrade pip
RUN pip install pipenv && pipenv install --dev --system --deploy
COPY . /code/
```

    2. In the work directory of your local machine, create *docker-compose.yml* with the content below: 

```
services:
  db: # This name is the host for DATABASE in setting.py in fathom_FEinterface
    image: postgres
    container_name: fathom_db
    environment:
      - POSTGRES_DB=fathom # This should be the same as the database name in the DATABASE in setting.py in fathom_FEinterface
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    ports:
        - "5432:5432"
  web:
    # This line trigger the 
    build: .
    volumes:
      - .:/code
    ports:
      - "8000:8000"
    image: web:v0.0
    container_name: fathom-web
    command:
      sh -c "python manage.py migrate &&
             python manage.py runserver 0.0.0.0:8000"
    depends_on:
      - db
```
    3. In the work directory of your local machine, create images and then containers using:\
`docker-compose up` \
You will be waiting for quite a while, after which you can run 127.0.0.1:8000 to test if it works\

2. Transfer file to server
    1. In the work directory of your local machine, save the Docker image/images as a .tar (zipped) file: (Note multiple images can be saved in one .tar file)\
`docker save -o <path for generated tar file> <image name> <image name> <image name>`\
You should add filename (not just directory) with -o, for example:\
`docker save -o fathom.tar fathom_web:v0.0 fathom_db:v0.0`
    2. Then copy the .tar file to a server (one of our number crunchers) with any file transfer approach you like.
    3. On the server, load(unzip) the .tar file into images:\
`docker load -i <path to image tar file>`\
for example:
`docker load -i fathom.tar`
it will renders two images: fathom_web:v0.0 fathom_db:v0.0

    4. Under any folder you like to work with on the server, create a new file named 'docker-compose.yml' with the following content.
This 'docker-compose.yml' file will help
```
services:
  db:
    image: postgres:latest
    container_name: fathom_db
    environment:
      - POSTGRES_DB=fathom
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    ports:
        - "5432:5432"
  web:
    ports:
      - "8000:8000"
    image: web:django
    container_name: fathom-web
    environment:
      - POSTGRES_DB=fathom
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    command: 
    # sh -c "..." allows multiple commands
      sh -c "python manage.py migrate &&
             python manage.py runserver 0.0.0.0:8000"
    depends_on:
      - db
```
    5. Under the same folder of the 'docker-compose.yml' file on the server, create containers from images using:\
`docker-compose up`
    6. Try 127.0.0.1:8000 to see if it works



# Tricks
https://stackoverflow.com/questions/44694086/when-run-docker-compose-up-i-get-python-cant-open-file-manage-py-errno-2
