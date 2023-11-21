FROM python:3.7-alpine
WORKDIR /app
COPY . /app
RUN pip install -r requirements.txt
EXPOSE 5000
CMD ["python", "app.py"]

# Docker build command: docker build -t jason .
# Docker run command: docker run -d -p 5001:5000 jason
# Docker images
# Docker ps
# Docker stop [CONTAINER ID]
# Need to rebuild the image if updates, then docker run -p port:port