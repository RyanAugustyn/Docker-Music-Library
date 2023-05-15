FROM node:current-alpine3.17
WORKDIR /user/src/app/frontend
COPY . . 
RUN npm install

#########################
React.js Dockerfile

A breakdown of the recommended React.js Dockerfile structure.
Recommended React.js Dockerfile Structure

FROM node:14.20.1-alpine3.15 as build
WORKDIR /app
COPY package*.json ./
RUN npm ci --silent
RUN npm install react-scripts@3.4.1 -g --silent
COPY . ./
RUN npm run build

FROM nginx:stable-alpine
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;"]

File Breakdown

Here's a breakdown of each line in the Dockerfile with a brief explanation of its purpose:

FROM node:14.20.1-alpine3.15 as build

This line sets the base image for the Docker container as Node.js version 14.20.1 on Alpine Linux 3.15 and also sets an alias build to reference this image.

WORKDIR /app

This line sets the working directory within the container to /app. Any commands that follow will be executed in this directory.

COPY package*.json ./

This line copies the package.json and package-lock.json files from the current directory on the host machine into the /app directory in the container.

RUN npm ci --silent

This line runs the npm ci command to install the dependencies specified in the package-lock.json file. The --silent flag suppresses any log messages during installation.

RUN npm install react-scripts@3.4.1 -g --silent

This line installs the react-scripts package globally using npm install. This package provides a collection of scripts and tools used to build and run React applications. The --silent flag suppresses any log messages during installation.

COPY . ./

This line copies all files and directories from the current directory on the host machine into the /app directory in the container.

RUN npm run build

This line runs the npm run build command to build the React application. This typically compiles the application code into static files that can be served by a web server.

FROM nginx:stable-alpine

This line sets the base image for the second stage of the Docker container as Nginx on Alpine Linux. This creates a new stage in the container, independent of the first stage.

COPY --from=build /app/build /usr/share/nginx/html

This line copies the compiled static files from the first stage (specified by the --from=build flag) into the default Nginx HTML directory (/usr/share/nginx/html) in the second stage.

EXPOSE 80

This line exposes port 80 on the container, allowing it to be accessed by other containers or the host machine.

CMD ["nginx", "-g", "daemon off;"]

This line specifies the command to run when the container is started. In this case, it starts the Nginx web server with the daemon off; flag to keep the server running in the foreground.
 
Modifying the Docker NGINX Build to Handle React Router

When a React application uses React Router to enable URL pathing, there is a need for further customization when using an NGINX image to serve the React app’s production build. 

The problem is the behavior of the default config file. If you were to go to some URL with a specific path such as:

www.somesite.com/login

The default configuration file would look for an html file called:

login.html

Because our React apps are SPAs, we instead need the NGINX configuration file to NOT look for a separate login.html file and simply route back to the index.html file.
 

This is accomplished by defining a custom NGINX configuration file in the React application’s root directory. We then need to copy this new NGINX configuration file to the NGINX image at image build time so that the image uses our custom NGINX configuration rather than the default one that ships with the NGINX base image.

To do this, create a new file in your React applications root directory called custom-nginx.conf . Place the following code into this new file:

server {
    listen 80;
    server_name localhost;

    location / {
        root /usr/share/nginx/html;
        try_files $uri /index.html;
    }
}

This file will specify that when any URL path is requested, such as www.somesite.com/login, it will always default the request back to the index.html rather than looking for a login.html file.

Now that we have this file created and placed in the same directory as our application’s Dockerfile, we need to copy it over to the image in the Dockerfile instructions using this line:

COPY custom-nginx.conf /etc/nginx/conf.d/default.conf

The final result of your Dockerfile should be as follows:

FROM node:14.20.1-alpine3.15 as build
WORKDIR /app
COPY package*.json ./
RUN npm i
RUN npm install react-scripts@3.4.1 -g --silent
COPY . ./
RUN npm run build

FROM nginx:stable-alpine
COPY custom-nginx.conf /etc/nginx/conf.d/default.conf
COPY --from=build /app/build /usr/share/nginx/html
EXPOSE 80
CMD ["nginx", "-g", "daemon off;