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



docker-compose up --build is going to create the images based off the instructions.
Docker compose automatically detects change. This is because of what we described in the yaml file, which was volumes, which will allow the OS to detect and push changes. 

docker-compose up -d can also do detach
To stop these, docker-compose down

