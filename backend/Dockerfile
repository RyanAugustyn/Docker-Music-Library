FROM python:alpine3.18
WORKDIR /user/src/backend
COPY requirements.txt ./
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
#CMD [ "flask", "run", "--host=0.0.0.0" ]

####################


 Flask Dockerfile

A breakdown of the recommended Flask REST API Dockerfile structure.


FROM python:alpine3.17
WORKDIR /users/src/app
COPY requirements.txt ./
RUN pip install -r requirements.txt
COPY . .
EXPOSE 5000
CMD ["flask", "run", "--host=0.0.0.0"]

 
File Breakdown

Here's a breakdown of each line in the Dockerfile with a brief explanation of its purpose:

FROM python:alpine3.17

This line specifies the base image that the Docker image being built will be based on. In this case, it's the Alpine Linux version of the Python programming language.

WORKDIR /users/src/app

This line sets the working directory to /users/src/app inside the container. This is where any subsequent commands will be executed from.

COPY requirements.txt ./

This line copies the requirements.txt file from the host (i.e., the machine building the Docker image) to the current working directory inside the container.

RUN pip install -r requirements.txt

This line installs the Python packages specified in requirements.txt inside the container.

COPY . .

This line copies all the files and directories from the host to the current working directory inside the container. This includes the source code for the application.

EXPOSE 5000

This line exposes port 5000 in the container. This means that the container will be able to receive incoming network traffic on port 5000.

CMD ["flask", "run", "--host=0.0.0.0"]

This line specifies the default command to run when the container starts. In this case, it's running the Flask development server on the IP address 0.0.0.0 and port 5000.