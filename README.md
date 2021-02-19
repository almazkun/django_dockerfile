# django_dockerfile
Dockerfile to quickly run some Django app

```Dockerfile
FROM python:buster

WORKDIR /usr/src/code

EXPOSE 8000

RUN apt-get update && apt-get -y upgrade

ENV PYTHONDONTWRITEBYTECODE 1

ENV PYTHONUNBUFFERED 1

RUN pip3 install --upgrade pip

RUN pip3 install pipenv

COPY Pipfile ./

RUN pipenv lock

RUN pipenv install --system

COPY . .

CMD ["python3", "manage.py", "runserver", "0.0.0.0:8000"]
```

## Build
```bash
docker build -t d_django .
```

## Run
```bash
docker run -p 8000:8000 --name dj d_django
```

### Some docker commands
1. Remove all images not referenced by any container
```bash
docker image prune -a
```
2. Remove all stopped containers
```bash
docker container rm $(docker container ls -aq)
```
