# docker_flask_homework
This is a repository for Assignment 7 in HHA504, Docker. 

## Setting Up and Dockerizing a Flask App

We created a simple Flask application called app.py
```
from flask import Flask

app = Flask(__name__)

@app.route('/')
def hello_world():
    return 'Hello, World! From a Flask app in a Docker container!'

if __name__ == '__main__':
    app.run(debug=True, host='0.0.0.0', port=5000)
```

We also created a requirements.txt file that contains flask.
Finally, we created a Dockerfile that contained the image we are trying to make.
```
FROM python:3.7-alpine
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python", "app.py"]
```
* "From" chooses the base image for the Docker image. 
* "WORKDIR /app" sets the working directory inside the container to '/app'
* "COPY . /app" copies the contents of the current directory to the /app located inside the container
* "RUN pip install -r requirements .txt" installs the python dependencies listed in the requirements.txt file
* "EXPOSE 5000" makes the container on port 5000
* "CMD ["python", "app.py"]" runs the app.py

Next, in the shell, we run the following command.
```
Docker build command: docker build -t jason .
```
This names our app, "jason". 

Then run: 
```
Docker run command: docker run -d -p 8000:5000 jason
```
-d runs the app in a detached mode, so the app runs in the background. 
-p will choose a port. For this instance, we chose port 8000 as the docker with 5000 as the base. 
Finally, we name our app. 

```
Docker images
```
Docker images will let us see what images we have built.

```
Docker ps
```
Will allow us to see which images we've activated. 

```
Docker stop [CONTAINER ID]
```
Will allow us to stop the container given the container id. 

![](https://github.com/jas-tang/docker_flask_homework/blob/main/images/1.JPG)

![](https://github.com/jas-tang/docker_flask_homework/blob/main/images/2.JPG)

![](https://github.com/jas-tang/docker_flask_homework/blob/main/images/3.JPG)

![](https://github.com/jas-tang/docker_flask_homework/blob/main/images/4.JPG)

We can see our app run on port 8000.

In order to edit the flask apps, we will need to rebuild the image again. 

```
docker run -p port:port
```

To re run. 

## Preparing Two Flask Applications

We create two separate flask apps, each with its own requirements and dockerfiles. They are in separate folders. 

We then set up a docker-compose.yml on the same level as the folders that hold each flask app respectively.

This is the setup: 

![](https://github.com/jas-tang/docker_flask_homework/blob/main/images/5.JPG)

The following is the docker-compose.yaml file:
```
version: '3'
services:
  flask_app_1:
    build: ./flask1
    ports:
      - "5001:5000"
    volumes:
      - ./flask1:/app
  flask_app_2:
    build: ./flask2
    ports:
      - "5002:5000"
    volumes:
      - ./flask2:/app
```
* Version 3 specifies the v ersion of the Docker Compose file
* Services chooses the containers that make up the application. For our case, its flask 1 and flask 2
* Build specifies the build for each service
* The Ports are the ports we choose to host the flask apps
* Volumes will allow the OS to detect and push changes. 

Now, we move on to work in the shell.

```
docker-compose up --build
```

We can also run with detach. 

```
docker-compose up -d
```

To stop these, 

```
docker-compose down
```

![](https://github.com/jas-tang/docker_flask_homework/blob/main/images/6.JPG)

![](https://github.com/jas-tang/docker_flask_homework/blob/main/images/7.JPG)

![](https://github.com/jas-tang/docker_flask_homework/blob/main/images/8.JPG)

![](https://github.com/jas-tang/docker_flask_homework/blob/main/images/9.JPG)

