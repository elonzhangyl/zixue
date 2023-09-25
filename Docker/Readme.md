# Dockerfile
```
FROM python:3.8

# Setup env
ENV LANG C.UTF-8
ENV LC_ALL C.UTF-8
ENV PYTHONDONTWRITEBYTECODE 1
ENV PYTHONFAULTHANDLER 1

WORKDIR /code/

# Install & use pipenv
COPY Pipfile Pipfile.lock /code/
RUN python -m pip install --upgrade pip
RUN pip install pipenv && pipenv install --dev --system --deploy

COPY . /code/
```
# docker-compose.yml
```
services:
  db: # This name is the host for DATABASE in setting.py in fathom_FEinterface
    image: postgres
    # volumes:
    #   - ./data/db:/var/lib/postgresql/data
    environment:
      - POSTGRES_DB=fathom # This database name should be the same as in the DATABASE in setting.py in fathom_FEinterface
      - POSTGRES_USER=postgres
      - POSTGRES_PASSWORD=postgres
    ports:
        - "5432:5432"
  web:
    build: .
    volumes:
      - .:/code
    ports:
      - "8001:8001"
    command: python manage.py runserver 0.0.0.0:8001
    depends_on:
      - db
```
# Transfer file to server
You will need to save the Docker image as a tar file:\
`docker save -o <path for generated tar file> <image name>`\
Then copy your image to a new system with regular file transfer tools such as cp, scp, or rsync (preferred for big files). After that you will have to load the image into Docker:\
`docker load -i <path to image tar file>`\
You should add filename (not just directory) with -o, for example:\
`docker save -o c:/myfile.tar centos:16`\
